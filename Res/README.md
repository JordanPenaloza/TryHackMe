1.) Res is a CTF box where we will need to hack into a vulnerable database server with an in-memory data-structure 
  - Let's run an nmap scan to see what ports we can find
  - nmap -sC -sV didn't work this time so we did a basic nmap scan with no parameters

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/346974ec-8827-424a-8cde-363348e861dc)

  - The only port open is 80 which is HTTP so let's check out the page
    
![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/58f1167e-3f06-4c85-8e5d-5f1f3b5171b5)


  -  Just a simple apache server, maybe we can check for hidden directories?
2.) Let's do a gobuster scan

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/20cf9f09-8fd7-4a45-b4a0-e074bacfae3d)

  -  Nothing of interest at all? Maybe we can take a step back with nmapping even further
3.) Let's check all 65k ports

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/99683ce5-2ea7-4a7b-b5fe-969de4c78ba3)

  - Looks like we found another port 6379 for Redis db on version 6.0.7
  - Searchsploit lets us know that redis is vulnerable to unauthenticated code execution which is typically linked to reverse shells
  - SSH is not open so we can't upload a file there. Maybe a web shell?

3.) Connecting to redis

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/37d5cc63-778a-4047-bc27-f0b14be6ddde)

  - After doing some research I found this command and found we could enter the server without authentication
  - We also see a possible username "vianka" which we can probably use later
  - https://book.hacktricks.xyz/pentesting/6379-pentesting-redis I found this post which showed hown vulnerable redis is to interactive shells
  - We can run the following sequence of commands to set the dbfilename to shell.php

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/8bb810bf-f595-4810-b4ad-522fa6f9660a)

  - Lets set up a netcat listener

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/c256ccea-053e-410b-9375-4adc839c5095)


  - now we can issue command injection in the web browser by visiting the /redis.php directory

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/40a81411-5987-44c0-b4c3-5635f2424bdc)

4.) Let's upgrade our shell by running python3 -c 'import pty;pty.spawn("/bin/bash:)'

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/1581366e-412e-41b5-97c6-62b3664b71a9)

  - We then found the user flag using the userflag we found earlier

5.) Root time

  - We can run find / -perm /4000 -type f 2> /dev/null to look for files that may have the SUID bit set
    
![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/e6b3b7d3-7b30-4fde-b1e0-caa491f39843)

  - /xxd looks a little out of place, GTFObins tells us that we can read shadow files by running xxd /etc/shadow | xxd -r
    
![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/761ac09c-c694-447c-b073-9510bc6b8a15)

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/b3361fbe-190d-4d94-bd3f-74e8ec9a94e2)

  - We can use hashcat to crack the password

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/8c1cfb23-7b97-4c4b-bf7b-98847eaccb4e)

  - We got a password! Let's login

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/2e208b30-f158-4d97-a29f-95cc86d3ef11)

  - We're in and I used sudo -i to switch to root
  - we can ls for the root flag and that is all!





   













