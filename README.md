# linux-priv-Esc

# GTFOBins  
https://gtfobins.github.io

018 

# Initial Enumeration
uname -a, netstat -ano

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


File-Permission => search for weak file permission 
