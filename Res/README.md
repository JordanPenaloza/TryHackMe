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

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/49f54c05-91a6-4a72-ad8f-c435af2d5c49)

Lets set up a netcat listener

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/90a804d6-3be3-4274-8104-601fcde0874c)

Now change test to "php system get command here" using the redis-cli

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/1d674983-0d59-48c0-a2a1-636deae5f8ed)

now we can issue command injection in the web browser

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/8bb810bf-f595-4810-b4ad-522fa6f9660a)

Now we have a shell on the host











