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
  - Let's try to crack Rick's password
  - 

