ok so my old readme got deleted so this is gonna be a little bit of a lazy readme LETS GO

1.) We have been asked by the tompany to perform a penetration test on their system so let's go and nmap scan wahoooo

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/bf83bffc-d432-42bb-9135-3a8d4defbc4f)

   - We found http, ssh, and ftp open with an anonymous ftp login allowed so let's check that out
   - We can login to ftp as anonymous and retrieve all the files found by doing the following below
   - ![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/c6696ef3-ffa5-4b10-b28d-3138ac1aa1be)
   - After opening the notice.txt file we foound we found a username Maya
     
2.) Let's find hidden directories of the http server using gobuster

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/03d350c0-7c11-4896-ab42-2aef613e3765)

  - We found the /files directory, let's check it out


