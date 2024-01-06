# Linux 101

## Description

For this challenge, I ventured to *Santa's Surf Shack* on *Christmas Island* and spoke to the elf *Ginger Breddie* to start the challenge. 

![Figure 1: Opening Prompt for Linux 101 Challenge](/img/linux-101-description.png)

## Prompts and Answers

1. Perform a directory listing of your home directory to find a troll and retrieve a present!

**Answer**:

```bash
ls | grep troll
```

![Figure 2: Directory Listing Command](/img/linux-101-1.png)

2. Now find the troll inside the troll.

**Answer**:

```bash
cat troll_19315479765589239
```

![Figure 3: Reading the Contents of `troll_19315479765589239` from the CLI](/img/linux-101-2.png)

3. Great, now remove the troll in your home directory.

**Answer**:

```bash
rm troll_19315479765589239
```

![Figure 4: Removing the File `troll_19315479765589239` from the `/home/elf` Directory](/img/linux-101-3.png)

4. Print the present working directory using a command.

**Answer**:

```bash
pwd
```

![Figure 5: Printing the Present Working Directory](/img/linux-101-4.png)

5. Good job but it looks like another troll hid itself in your home directory. Find the hidden troll!

**Answer**:

```bash
ls -a | grep troll
```

![Figure 6: Finding a Hidden File in the `/home/elf` Directory](/img/linux-101-5.png)

6. Excellent, now find the troll in your command history.

**Answer**:

```bash
cat .bash_history | grep troll
```

> *Note*:
> Another suitable answer here would be to run `history | grep troll`. However, since this command would include commands run in the current session, and we can reasonably deduce that this question is looking for a troll from a previous session used to set up this host, it is better to inspect the contents of `.bash_history`, which would only contain commands from a concluded session.

![Figure 7: Checking the Bash History of *elf*](/img/linux-101-6.png)

7. Find the troll in your environment variables.

**Answer**:

```bash
env | grep troll
```

![Figure 8: Checking Environment Variables](/img/linux-101-7.png)

8. Next, head into the `workshop`.

**Answer**:

```bash
cd workshop/
```

![Figure 9: Changing Directories to `/home/elf/workshop`](/img/linux-101-8.png)

9. A troll is hiding in one of the workshop toolboxes. Use `grep` while ignoring case to find which toolbox the troll is in.

**Answer**:

```bash
cat *.txt | grep -i troll
```

![Figure 10: Filtering the Results of `ls` While Ignoring Case](/img/linux-101-9.png)

10. A troll is blocking the `present_engine` from starting. Run the `present_engine` binary to retrieve this troll.

**Answer**:

```bash
chmod +x present_engine 
./present_engine 
```

> *Note*:
> The command `chmod +x` will give execute permissions to *all* users of the host. This may not be ideal from a security perspective, so another alternative command would be `chmod `, which would only give execute permissions to the owner of the file while maintaining read access for other users. 

![Figure 11: Modifying the ACL of the `/home/elf/workshop/present_engine` Binary and Executing it](/img/linux-101-10.png)

11. Trolls have blown the fuses in `/home/elf/workshop/electrical`. `cd` into `electrical` and rename `blown_fuse0` to `fuse0`.

**Answer**:

```bash
cd /home/elf/workshop/electrical/
mv blown_fuse0 fuse0
```

![Figure 12: Renaming `blown_fuse0` to `fuse0`](/img/linux-101-11.png)

12. Now, make a symbolic link (symlink) named `fuse1` that points to `fuse0`.

**Answer**:

```bash
ln -s fuse0 fuse1
```

![Figure 13: Creating a Symbolic Link `fuse1` Pointing to `fuse0`](/img/linux-101-12.png)

13. Make a copy of `fuse1` named `fuse2`.

**Answer**:

```bash
cp fuse1 fuse2
```

![Figure 14: Making a Copy of `fuse1`](/img/linux-101-13.png)

14. We need to make sure trolls don't come back. Add the characters "TROLL_REPELLENT" into the file `fuse2`.

**Answer**:

```bash
echo TROLL_REPELLENT >> fuse2
```

![Figure 15: Appending the string "TROLL_REPELLENT" to `fuse2`](/img/linux-101-14.png)

15. Find the troll somewhere in `/opt/troll_den`.

**Answer**:

```bash
find /opt/troll_den -iname "*troll*"
```

![Figure 16: Finding the Troll in `/opt/troll_den`](/img/linux-101-15.png)

16. Find the file somewhere in `/opt/troll_den` that is owned by the user *troll*.

**Answer**:

```bash
find /opt/troll_den -user troll
```

![Figure 17: Finding the File Owned by *troll* in `/opt/troll_den`](/img/linux-101-16.png)

17. Find the file created by trolls that is greater than 108 kilobytes and less than 110 kilobytes located somewhere in `/opt/troll_den`.

**Answer**:

```bash
find /opt/troll_den -size +108k -size -110k
```

![Figure 18: Finding a File Between 108 KB and 110 KB](/img/linux-101-17.png)

18. List running processes to find another troll.

**Answer**:

```bash
ps aux
```

![Figure 19: Listing Running Processes](/img/linux-101-18.png)

19. The `14516_troll` process is listening on a TCP port. Use a command to have the only listening port display to the screen.

**Answer**:

```bash
netstat -tln
```

![Figure 20: Displaying the TCP Port Listening on the Loopback Address](/img/linux-101-19.png)

20. The service listening on port 54321 is an HTTP server. Interact with this server to retrieve the last troll.

**Answer**:

```bash
curl http://127.0.0.1:54321
```

![Figure 21: Interacting with the Locally Running Web Service](/img/linux-101-20.png)

21. Your final task is to stop the `14516_troll` process to collect the remaining presents.

**Answer**:

```bash
ps aux | grep 14516_troll
kill 28772
```

![Figure 22: Finding and Stopping the `14516_troll` Process](/img/linux-101-21.png)

22. Congratulations, you caught all the trolls and retrieved all the presents! Type "exit" to close...

**Answer**:

```bash
exit
```
