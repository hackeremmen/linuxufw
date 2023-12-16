# linuxufw


								TryHackMe - Intrusion detection To the Pots, Through the Walls 
								==============================================================


root@ip-10-10-172-106:~# ssh vantwinkle@10.10.19.134 
The authenticity of host '10.10.19.134 (10.10.19.134)' can't be established.
ECDSA key fingerprint is SHA256:Xa8iaSS27Lp9yoIN+A6pApvLdCONcUGwhtLmEV9h0bE.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '10.10.19.134' (ECDSA) to the list of known hosts.
vantwinkle@10.10.19.134's password: 
Welcome to Ubuntu 20.04.6 LTS (GNU/Linux 5.15.0-1049-aws x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Sat Dec 16 18:04:20 UTC 2023

  System load:  0.0               Processes:             122
  Usage of /:   6.3% of 58.09GB   Users logged in:       0
  Memory usage: 15%               IPv4 address for eth0: 10.10.19.134
  Swap usage:   0%

 * Ubuntu Pro delivers the most comprehensive open source security and
   compliance features.

   https://ubuntu.com/aws/pro

Expanded Security Maintenance for Applications is not enabled.

0 updates can be applied immediately.

3 additional security updates can be applied with ESM Apps.
Learn more about enabling ESM Apps service at https://ubuntu.com/esm


The list of available updates is more than a week old.
To check for new updates run: sudo apt update

Last login: Wed Nov 15 01:55:25 2023 from 10.9.3.14
vantwinkle@ip-10-10-19-134:~$ sudo ufw status
[sudo] password for vantwinkle: 
Status: inactive
vantwinkle@ip-10-10-19-134:~$ sudo ufw default allow outgoing
Default outgoing policy changed to 'allow'
(be sure to update your rules accordingly)
vantwinkle@ip-10-10-19-134:~$ sudo ufw default deny incoming
Default incoming policy changed to 'deny'
(be sure to update your rules accordingly)
vantwinkle@ip-10-10-19-134:~$ sudo ufw  allow 22/tcp
Rules updated
Rules updated (v6)
vantwinkle@ip-10-10-19-134:~$ sudo ufw deny from 192.168.100.25
Rules updated
vantwinkle@ip-10-10-19-134:~$ sudo ufw deny in on eth0 from 192.168.100.26
Rules updated
vantwinkle@ip-10-10-19-134:~$ sudo ufw enable
Command may disrupt existing ssh connections. Proceed with operation (y|n)? y
Firewall is active and enabled on system startup
vantwinkle@ip-10-10-19-134:~$ sudo ufw status verbose
Status: active
Logging: on (low)
Default: deny (incoming), allow (outgoing), disabled (routed)
New profiles: skip

To                         Action      From
--                         ------      ----
22/tcp                     ALLOW IN    Anywhere                  
Anywhere                   DENY IN     192.168.100.25            
Anywhere on eth0           DENY IN     192.168.100.26            
22/tcp (v6)                ALLOW IN    Anywhere (v6)             

vantwinkle@ip-10-10-19-134:~$ ls
Van_Twinkle_rules.sh  pentbox  sudo
vantwinkle@ip-10-10-19-134:~$ cd pentbox/
vantwinkle@ip-10-10-19-134:~/pentbox$ ls
README.md  pentbox-1.8  pentbox.tar.gz
vantwinkle@ip-10-10-19-134:~/pentbox$ cd pentbox-1.8/
vantwinkle@ip-10-10-19-134:~/pentbox/pentbox-1.8$ ls
COPYING.txt  changelog.txt  lib  other  pb_update.rb  pentbox.rb  readme.txt  todo.txt  tools
vantwinkle@ip-10-10-19-134:~/pentbox/pentbox-1.8$ sudo ./pentbox.rb

 PenTBox 1.8 
             .__.
             (oo)____
             (__)    )--*
                ||--|| 

--------- Menu          ruby2.7.0 @ x86_64-linux-gnu

1- Cryptography tools

2- Network tools

3- Web

4- Ip grabber

5- Geolocation ip

6- Mass attack

7- License and contact

8- Exit

   -> 2

1- Net DoS Tester
2- TCP port scanner
3- Honeypot
4- Fuzzer
5- DNS and host gathering
6- MAC address geolocation (samy.pl)

0- Back

   -> 3

// Honeypot //

You must run PenTBox with root privileges.

 Select option.

1- Fast Auto Configuration
2- Manual Configuration [Advanced Users, more options]

   -> 2

 Insert port to Open.

   -> 8080

 Insert false message to show.

   -> Santa has gone for the Holidays. Tough luck.

 Save a log with intrusions?

 (y/n)   -> y

 Log file name? (incremental)

Default: */pentbox/other/log_honeypot.txt

   -> 

vantwinkle@ip-10-10-19-134:~$ sudo nano Van_Twinkle_rules.sh
#!/bin/bash
sudo ufw --force reset
sudo ufw default allow incoming
sudo ufw allow http 
sudo ufw allow ssh
sudo ufw deny 21/tcp
sudo ufw deny from any to any port 8088
sudo ufw deny 8090/tcp
sudo ufw enable 


#!/bin/bash
sudo ufw --force reset
sudo ufw default allow incoming
sudo ufw allow http 
sudo ufw allow ssh
sudo ufw deny 21/tcp
sudo ufw deny from any to any port 8088
sudo ufw allow 8090/tcp
sudo ufw enable 


THM{P0T$_W@11S_4_S@N7@} 
