Vitctim IP: 10.10.69.111

1.) Scanning
  - The first thing we always want to do when scanning through an IP is using nmap to look for open ports

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/2960aed8-b649-4c34-ba77-1912c9f6e85b)

  - -sC: This option enables the Nmap script scanning. Nmap comes with a variety of scripts that can be used to perform specific tasks during a scan. The -sC option tells Nmap to run default scripts against the target.

  - -sV: This option enables version detection for services running on open ports. Nmap tries to determine the software and version of the services by sending specific probes to those services and analyzing the responses.

  Putting both options together, the nmap -sC -sV command performs a comprehensive scan, attempting to identify open ports, running services, and their versions. The script scanning (-sC) can provide additional information     by running predefined scripts to gather more details about the services or vulnerabilities they may have.

  - port 22 and 80 are open which correspond to ssh and http. We can probably use the open ssh port to find a way into the machine via user credentials
  - port 80 signifies that there is a web server running on apache. Let's visit it to see what we can find

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/53fcf720-89e1-4eec-9105-72e7b8c998af)

  - We need to find the 3 fkags mentioned in the web page but we also need to find a password
  - Maybe we can find something useful in page source?

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/d6a2adb9-14e4-4b09-b879-cf7819209894)

  - We got a username!, we might be able to use that as a username to login with the ssh port and we can find a password using a brute force attacker like hydra
  - username: R1ckRul3s

2.) Enumeration

  - Let's enumerate through the webpage using gobuster to find other directories in the webpage

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/423ed639-82b6-4b92-bf53-0379947ec9ad)

  - We found /robots.txt and /assets
  - Let's visit them to see what we can find

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/5a5a16ac-50be-451c-a84c-84b94ba450df)

  - Hmmm, this could be a password?

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/b0fd20dc-5651-4f13-8e63-25a7e90edf4c)

  - Well it's just a bunch of gifs so not very interesting unless there is data hidden in the images but I doubt it
  - There must be more so let's use gobuster again but scan for php and html directories

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/ee00e4d0-96ee-4716-966c-3c92146a47ec)

  - There we go, there's a login page
  - Maybe we can use the username and possible password we found?

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/fbaf214a-fab4-43be-920a-d3e23a2b9b76)

  - We can only really access the commands panel which means we can possibly inject a reverse shell to connect to the system
    
![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/f3ba4c7b-bcf5-410b-a84c-1aa66ba9a405)

  - I ran a -ls command and it seems this is a linux based command panel
![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/bb4c6a2c-d38c-4e78-a63b-1455d8c500b8)

  - I tried to cat one of the files and I have no permissions

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/e1a4798f-08f0-49d1-8d89-82618d722d51)

  - We can open the flag txt in the directory instead of using cat however, here is the first flag
  - Considering we were able to view the files in a different directory, we can probably use directory traversal to move up to root

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/360f4a75-b16c-4463-bdaf-b848afaceb73)

  - I was right!
  - ls -al prints all the files in long mode to see permissions
  - pwd prints the working directory
    
![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/b3a4c7bd-44b6-4020-b422-812eb9d6a835)

  - /home is typically where all linux user's files are
  - Here we see /rick and /ubuntu

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/95f136d1-8054-4cac-abc7-34ac99db8f53)

  - Going to the rick directory we can see the second ingredients file

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/1e68c7eb-a07a-476b-9a34-f5551188b0b6)

  - We can use the less command to show the contents of second ingredients to find the second flag

3.) Privelage Escalation

  - We can run sudo -l to display what sudo commands we can execute

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/7f923183-4baf-4931-a89c-9deba8a12630)

  - Wow we can execute ANY sudo command which is awful security. That means there are many ways to us to gain root access
  - Well that was easy... we could just run a sudo ls command to find the 3rd flag

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/5a42829e-8451-4609-9092-e44fe293e167)

  - We may not be able to use the cat command but we can use sudo less to display the contents of the 3rd.txt file
  - We now have all 3 flags!







