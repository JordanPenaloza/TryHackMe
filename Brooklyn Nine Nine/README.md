Brooklyn Nine Nine is a CTF designed for beginner hackers. Let's see if we can do this without a write up's help
victim IP: 10.10.193.49
attack machine IP: 10.2.109.120 

1.) Scanning
  - Let's nmap scan this IP to search for open ports

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/398887a5-efa9-49b2-8966-769bccd0ada1)

  - FTP is open with anonymous login allowed
  - SSH is open
  - HTTP server is being hosted
    
![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/a3b660e1-f6aa-41f7-9f23-397c58159658)

  - Viewing the pages source code gives us a hint about steganography which is the act of hiding data in plain site
  - This means there must be some information in the image shown in the webpage. Let's dig a little deeper and try to get into the FTP port

2.) FTP port

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/09540cc4-790b-4242-881f-9aae340c9d94)

  - Since an anonymous login is allowed we can simply login to the ftp port using the anonymous username
    
![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/6e7bb2cb-da54-48eb-915e-1ab1bba5cec7)

  - We found a note to jake in the ftp and we transfered it to our machine and found that Jake's password is weak. We can possibly use Jake as a username and use hydra to crack his password in the ssh server?
  - Moving on, we saw the hint about steganography earlier so let's download the image from the webpage and dig deeper
    
![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/3fb010c2-8e34-447f-a463-085ddfd532b8)

  - Image downloaded but first I was to try hydra to crack jake's password

3.) SSH

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/cd9993f2-a559-49c3-8a62-d979f2a046c8)

  - we found jake's password! Let's login

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/0e1e59d9-a1cc-4e17-8609-9694a42053a9)

  - We're in! Let's see what we can do now

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/5bf2fd7b-6d19-48b4-9506-93d4182aff98)

  - Searching through the folders we found holt's folder which contained user.txt flag and a nano.save file

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/029c26da-f2e5-44c7-8249-cfdccc46a294)

  - We cannot access the nano.save file. That means it's privelage escalation time

4.) Privelage Escalation

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/135e2a29-0e0f-4eca-a2a0-8bdac0e13f08)

  - Running sudo -l gives us all the info we need
  - jake can run less commands as sudo, time to find root holes on gtfobins
    
![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/64a1baad-19d4-47cc-aa30-db854d9271c1)

  - We found a solution on gtfobins, lets try it out

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/db79db60-ea09-49ee-b405-b2d971cb12df)

  - I ran the 2nd command in the environment that popped up after running the less command and we escalated to root!
  - This CTF wasn't too bad but it was my first CTF that I completed without the assistance of a write up, I used my own learned knowledge!







