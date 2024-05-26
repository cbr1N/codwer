# Privelege Escalation Laboratory 2

## Privesc1

![image](https://github.com/cbr1N/codwer/assets/95069685/e5edacbe-cba4-4269-8594-1c49e55d6a07)

![image](https://github.com/cbr1N/codwer/assets/95069685/f0b16503-11a1-4912-a7cc-4d175fd94473)

![image](https://github.com/cbr1N/codwer/assets/95069685/09d4696a-5239-405e-8a24-e21387692d2e)

f the binary has the SUID bit set, it does not drop the elevated privileges and may be abused to access the file system, escalate or maintain privileged access as a SUID backdoor. If it is used to run sh -p, omit the -p argument on systems like Debian (<= Stretch) that allow the default sh shell to run with SUID privileges.

```
ls -la /usr/bin/find
./find . -exec /bin/sh -p \; -quit
whoami
cat /flag.txt
```
**flag: CWA{F1r5t_5U1D_D0N3}**

## Privesc2

![image](https://github.com/cbr1N/codwer/assets/95069685/ea0ec194-8a1d-448e-ad57-b710903254a0)

![image](https://github.com/cbr1N/codwer/assets/95069685/87373ef0-5f6c-4b35-bfe4-0b31f26feb18)

If the binary has the SUID bit set, it does not drop the elevated privileges and may be abused to access the file system, escalate or maintain privileged access as a SUID backdoor. If it is used to run sh -p, omit the -p argument on systems like Debian (<= Stretch) that allow the default sh shell to run with SUID privileges.

This example creates a local SUID copy of the binary and runs it to maintain elevated privileges. To interact with an existing SUID binary skip the first command and run the program using its original path.

Each input line is treated as a filename for the file command and the output is corrupted by a suffix : followed by the result or the error of the operation, so this may not be suitable for binary files.

```
ls -la /usr/bin/file
LFILE=/flag.txt
file -f $LFILE
```

**flag: CWA{G01NG_5TR0NG_K33P_1T_UP}**


## Privesc3

![image](https://github.com/cbr1N/codwer/assets/95069685/bc348785-5e18-4dfb-a312-6c5e29ab372c)

![image](https://github.com/cbr1N/codwer/assets/95069685/6bf9b740-1aab-4469-824f-4e302762faf1)

If the binary has the SUID bit set, it does not drop the elevated privileges and may be abused to access the file system, escalate or maintain privileged access as a SUID backdoor. If it is used to run sh -p, omit the -p argument on systems like Debian (<= Stretch) that allow the default sh shell to run with SUID privileges.

This can copy SUID permissions from any SUID binary (e.g., cp itself) to another.

**flag: CWA{ST1LL_G01NG_5TR0NG_K33P_1T_UP}**

## Privesc4

![image](https://github.com/cbr1N/codwer/assets/95069685/3a077765-b9ce-44f2-b2f0-0bc25422892e)

**flag: CWA{0N3_M0R3_SU1D_L3FT}**

## Privesc5

![image](https://github.com/cbr1N/codwer/assets/95069685/02ca44d2-e9ca-4737-937d-dd9377c8c8ee)

**flag: CWA{FLY_H1GH_L1K3_4_H4WK}**

## Privesc6

![image](https://github.com/cbr1N/codwer/assets/95069685/99601f0a-ed78-474a-a057-a1e968d5b1ce)

This line env_keep+=LD_PRELOAD means that when a user executes a command with sudo, the LD_PRELOAD environment variable will be preserved. This variable is often used to preload shared libraries before the standard ones, which can be useful for various purposes such as debugging or overriding certain functions.

![image](https://github.com/cbr1N/codwer/assets/95069685/354ea433-bf86-4c95-a717-d4108df8172b)

By creating a malicious ps script, we are taking advantage of the fact that run_me likely calls ps without specifying its full path, relying on the PATH environment variable.
Prepending /tmp to PATH ensures that our malicious ps script is executed instead of the system ps command.
This method works if run_me is running with elevated privileges, allowing our script to inherit these privileges and spawn a root shell.

**flag: CWA{K33P_Y0UR_P4TH_FULL}**

## Privesc7

![image](https://github.com/cbr1N/codwer/assets/95069685/eb07f96d-154e-441b-8e71-d42702feb046)

![image](https://github.com/cbr1N/codwer/assets/95069685/de4af3cc-f87e-406d-a705-8b6db3da8a44)

When a program is running, LD_PRELOAD loads a shared object before any others. By writing a simple script with init() function, it will help us execute code as soon as the object is loaded.

**flag: CWA{PR3L04D_Y0UR_L1BR4R135}**

## Privesc8

![image](https://github.com/cbr1N/codwer/assets/95069685/14ed8a1d-e0b9-4914-9e99-f5904a0beb3e)

![image](https://github.com/cbr1N/codwer/assets/95069685/4bb582be-68e1-43b8-9961-d961ce38ec96)

![image](https://github.com/cbr1N/codwer/assets/95069685/160d397a-db5c-44d3-92ae-9e543b59b717)

![image](https://github.com/cbr1N/codwer/assets/95069685/3720bafc-c7f0-447f-b2ce-64c08f04e2b9)

The LD_LIBRARY_PATH contains a list of directories which search for shared libraries first.
Use one of the shared objects in the list and we will hijack it by creating a file with same name. For this demonstration, we will be targeting the libcrypt.so.1 file.

**flag: CWA{KN0W_480U7_LD_L18R4RY_P47H}**
