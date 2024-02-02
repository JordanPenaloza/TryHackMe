The first step is to run an nmap scan to find open ports as shown below
![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/3ce22eb1-17e3-440f-b145-a04c9ee8e285)

Looks like we have a few ports open! We have ftp over port 21
ssh over port 22
and http over port 80

Looks like there is also an anonymous FTP login allowed which might be something to check out,
we found 2 textfiles, locks.txt and task.txt
![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/9c0f0523-3141-4fa8-b278-58d546c15aa4)

contents of locks.txt
![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/dafd58b3-f2e7-40bb-91b3-d7688d3cab50)
looks like a bunch of passwords!

contents of task.txt
![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/43880eb1-3742-4021-9706-f72bf449ba20)

We found the answer to questions #3! lin created the file!

Question 4 asks us what service we can use to bruteforce the text file found. Let's use ssh since port 22 is open
Question 5 asks us to find the user's password

We can use hydra to bruteforce attack the credentials by using the locks.txt file we found earlier
![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/ac0aac9a-3f21-4ea7-9883-6004cbad6001)

Success! we found the credentials for lin's account! RedDr4gonSynd1cat3
Now we can ssh into the account.
![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/c4854330-2a83-455e-963b-792a7893b62a)
We're in

Time to escalate
Let's try to see what sudo commands lin can use by running the following command 
![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/fb815180-207d-4dc5-a142-d66490f6bec8)

So lin can use the tar command, let's do some digging on GTFObins to see what we can find
![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/52393999-356d-47a9-b925-181f0b19a050)

Looks like this command will break us out of from this restricted environment
using sudo with this command gives us root privelages!!!
Now we can locate the root.txt file that was asked in the final question to get the flag
![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/894fdbfc-75f3-405e-b3a0-0e1af11e1111)

This CTF has taught me a lot about how FTP servers work and the many vulnerabilities associated with FTP











