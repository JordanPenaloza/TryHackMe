Mustacchio CTF
Victim IP: 10.10.102.63
Attack IP: 10.2.109.120  

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/192bcfeb-e1ea-4faf-87d2-41d5ab78e983)

  - Our nmap scan shows us that there is a webserver and ssh enabled. We also see a robots.txt file in the webserver

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/d75acdf6-86be-4b93-97f2-0be82e46ec29)

  - Gobuster shows us a few directories with robots.txt being 1 of them

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/2ea4c776-6f12-4640-9260-83bf79566541)

  - Going to the custom directory showed us users.bak lets download it

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/4fe35e70-4db1-4988-a7ca-e7acc771814c)

  - It's a DB backup folder
  - we can dump info about it and find the admin username and a hash
  - let's find a way to crack the hash

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/6b61f888-5d88-41f8-9894-25907b1f1fee)

  - using hashID we found the format of the hash to be most likely SHA-1
  - We can put the has in a hash.txt file and crack it with hashcat

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/7389dbec-3f24-4723-a66f-69aca1085964)

  - The mode of the hash is 100 and we were able to crack it this way

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/46b30147-61fd-4a61-8de4-2775000d5904)

  - Looks like ssh is disabled even though we have admin credentials, this might be a bit of trouble

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/daa3b994-8eef-4294-83ab-0bd1215a4f12)

  - We found another port! ultraseek-http port 8765

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/52078179-ee0d-48c9-a240-b0887c57e883)

  - Visitng the website with the port sent us to the admin login, we can login using our found credentials

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/bdc6da8e-1889-4ba2-b60a-eab664610c7f)

  - Viewing the page source we found a possible username, barry

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/d4b6f837-b47e-43e6-961f-95db89e30930)

  - We found a dontforget.bak file in the sourcecode and downloaded it and found that it was an XML file

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/1541296a-5489-4e8e-b959-cd62005d71ba)

  - Next we opened the xml file in gedit and found this

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/1c0fc21b-9c57-4ffe-a724-c9b547ed9103)

  - this website might be vulnerable to a XXE payload



  - ok i lost all my screenshots but I basically uploaded a XXE payload and was able to find the id_rsa hash key
  - I used john to turn it into a hash format and cracked it with john the ripper
  - I got into the ssh as barry and found user.txt
  - let's privelage escalate

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/1764b0d7-7285-4307-bb94-17b5db3c4a92)

  - The only interesting binary is live_log

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/493f08c8-27d5-4b0a-8b4a-5aec6a832d1d)

  - Looks like it's using the tails command but not the absolute path which is exploitable

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/e692f0bf-ea3e-4284-9c5a-658dfa03d947)

  - I wrote my own binary and added it to the live_log path and got root!






