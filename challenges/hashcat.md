# Hashcat

To complete this challenge, travel to *Scaredy Kite Heights* on the *Island of Misfit Toys* and talk to *Eve Snowflakes*.

This challenge invites us to attempt cracking a hash with the password recovery utility Hashcat.

## Challenge Prompt

After opening the terminal, we are greeted with a prompt explaining the premise of the challenge.

![Figure 1: Hashcat Challenge Prompt](/img/hashcat-prompt.png)

There are a few key takeaways here:
* Somewhere in our file system there is a kerberos token in some unknown hash format, and its type is related to an "ASREP Roast"
* The password recovery utility `hashcat` will be used to solve this challenge, and we are provided with command arguments to pass to the program, which we will analyze later
* We can use the [Hashcat Wiki's *Example hashes* page](https://hashcat.net/wiki/doku.php?id=example_hashes) to assist us in identifying hashes and their respective modes in Hashcat
* The [Hashcat CLI documentation](https://hashcat.net/wiki/doku.php?id=hashcat) may be useful in this challenge
* Once we have obtained the plaintext of the target hash, we will pass that plaintext to the binary `/bin/runtoanswer` to complete the challenge

## Identifying the Hash Type

What is the content of `hash.txt`?

```bash
cat hash.txt ; echo
```

![Figure 2: `hash.txt` Contents](/img/hash-txt.png)

This hash looks like the AS-REQ obtained from an AS-REP-roasting attack. Confirm this by going to https://hashcat.net/wiki/doku.php?id=example_hashes.

![Hashcat Example Hash Identified](/img/hashcat-examples-1.png)

What is AS-REP roasting?

## Cracking the Hash

How many passwords are in `password_list.txt`?

```bash
wc -l password_list.txt 
```

There are 143 passwords in the `password_list.txt` file.

We may want to add a rule file to our `hashcat` command to create more permutations of passwords and increase our odds of cracking the hash. Check what rules are pre-installed with `hashcat` by navigating the `/usr/share/hashcat/rules` directory.

```console
elf@8d59694afbd8:~$ ls /usr/share/hashcat/rules/
Incisive-leetspeak.rule                         combinator.rule     specific.rule
InsidePro-HashManager.rule                      d3ad0ne.rule        toggles1.rule
InsidePro-PasswordsPro.rule                     dive.rule           toggles2.rule
T0XlC-insert_00-99_1950-2050_toprules_0_F.rule  generated.rule      toggles3.rule
T0XlC-insert_space_and_special_0_F.rule         generated2.rule     toggles4.rule
T0XlC-insert_top_100_passwords_1_G.rule         hybrid              toggles5.rule
T0XlC.rule                                      leetspeak.rule      unix-ninja-leetspeak.rule
T0XlCv1.rule                                    oscommerce.rule
best64.rule                                     rockyou-30000.rule
```

Keep this in mind for later. For now, try to crack the hash without a rule list. Remember to prepend the arguments that SANS provided to the command

```console
elf@d0908ac20693:~$ hashcat -w 1 -u 1 --kernel-accel 1 --kernel-loops 1 -a 0 -m 18200 hash.txt password_list.txt --force

hashcat (v5.1.0) starting...

OpenCL Platform #1: The pocl project
====================================
* Device #1: pthread-Intel(R) Xeon(R) CPU @ 2.80GHz, 8192/30063 MB allocatable, 8MCU

Hashes: 1 digests; 1 unique digests, 1 unique salts
Bitmaps: 16 bits, 65536 entries, 0x0000ffff mask, 262144 bytes, 5/13 rotates
Rules: 1

Applicable optimizers:
* Zero-Byte
* Not-Iterated
* Single-Hash
* Single-Salt

Minimum password length supported by kernel: 0
Maximum password length supported by kernel: 256

ATTENTION! Pure (unoptimized) OpenCL kernels selected.
This enables cracking passwords and salts > length 32 but for the price of drastically reduced performance.
If you want to switch to optimized OpenCL kernels, append -O to your commandline.

Watchdog: Hardware monitoring interface not found on your system.
Watchdog: Temperature abort trigger disabled.

* Device #1: build_opts '-cl-std=CL1.2 -I OpenCL -I /usr/share/hashcat/OpenCL -D LOCAL_MEM_TYPE=2 -D VENDOR_ID=64 -D CUDA_ARCH=0 -D AMD_ROCM=0 -D VECT_SIZE=16 -D DEVICE_TYPE=2 -D DGST_R0=0 -D DGST_R1=1 -D DGST_R2=2 -D DGST_R3=3 -D DGST_ELEM=4 -D KERN_TYPE=18200 -D _unroll'
* Device #1: Kernel m18200_a0-pure.d7bc3268.kernel not found in cache! Building may take a while...
Dictionary cache built:
* Filename..: password_list.txt
* Passwords.: 144
* Bytes.....: 2776
* Keyspace..: 144
* Runtime...: 0 secs

The wordlist or mask that you are using is too small.
This means that hashcat cannot use the full parallel power of your device(s).
Unless you supply more work, your cracking speed will drop.
For tips on supplying more work, see: https://hashcat.net/faq/morework

Approaching final keyspace - workload adjusted.  

$krb5asrep$23$alabaster_snowball@XMAS.LOCAL:22865a2bceeaa73227ea4021879eda02$8f07417379e610e2dcb0621462fec3675bb5a850aba31837d541e50c622dc5faee60e48e019256e466d29b4d8c43cbf5bf7264b12c21737499cfcb73d95a903005a6ab6d9689ddd2772b908fc0d0aef43bb34db66af1dddb55b64937d3c7d7e93a91a7f303fef96e17d7f5479bae25c0183e74822ac652e92a56d0251bb5d975c2f2b63f4458526824f2c3dc1f1fcbacb2f6e52022ba6e6b401660b43b5070409cac0cc6223a2bf1b4b415574d7132f2607e12075f7cd2f8674c33e40d8ed55628f1c3eb08dbb8845b0f3bae708784c805b9a3f4b78ddf6830ad0e9eafb07980d7f2e270d8dd1966:IluvC4ndyC4nes!
                                                 
Session..........: hashcat
Status...........: Cracked
Hash.Type........: Kerberos 5 AS-REP etype 23
Hash.Target......: $krb5asrep$23$alabaster_snowball@XMAS.LOCAL:22865a2...dd1966
Time.Started.....: Sun Dec 31 19:06:31 2023 (0 secs)
Time.Estimated...: Sun Dec 31 19:06:31 2023 (0 secs)
Guess.Base.......: File (password_list.txt)
Guess.Queue......: 1/1 (100.00%)
Speed.#1.........:     1217 H/s (0.52ms) @ Accel:1 Loops:1 Thr:64 Vec:16
Recovered........: 1/1 (100.00%) Digests, 1/1 (100.00%) Salts
Progress.........: 144/144 (100.00%)
Rejected.........: 0/144 (0.00%)
Restore.Point....: 0/144 (0.00%)
Restore.Sub.#1...: Salt:0 Amplifier:0-1 Iteration:0-0
Candidates.#1....: 1LuvCandyC4n3s!2022 -> iLuvC4ndyC4n3s!23!

Started: Sun Dec 31 19:06:17 2023
Stopped: Sun Dec 31 19:06:33 2023
```

The password has been identified as *IluvC4ndyC4nes!*.

## Submitting the Answer

Run `/bin/runtoanswer` to submit the password.

```console
elf@d0908ac20693:~$ /bin/runtoanswer
What is the password for the hash in /home/elf/hash.txt ?

> IluvC4ndyC4nes!
Your answer: IluvC4ndyC4nes!

Checking....
Your answer is correct!
```

