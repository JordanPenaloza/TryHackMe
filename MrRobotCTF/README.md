![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/cf36963b-db3c-417f-8445-09cbb1959606)
10.10.122.230
  - HTTP open and ssh closed
  - The webpage is funny go check it out
  - We also have port 443 open for ssl

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/03f81a62-a156-4c57-be50-39d98565d6a8)

  - Lots of directories!!

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/d6b5fcb5-0d8e-4bb0-a868-b3aa79c7303d)

  - Visitng robots gives us a hint at where the key is. downloading key-1-of-3.txt gives us the first flag

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/61ead586-dc83-4353-bfb7-f4c28f4f4f59)

  - We also downloaded the fsocity dic and used it in hydra to find a username Elliot
  - for this we needed to us burpsuite to find the post request used and to see what string was sent to find a username
  - using hydra again we can brute force the password using the same method only with a username this time

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/f661c10d-9fca-48db-998a-e351dc0fe8f2)

  - Logging in we find an editor, this might be really bad since that usually means we can just input code to execute

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/decfdfab-46eb-42bd-8b7e-d1570b2ee24c)

  - I was right, we can simply input php code to give us a reverseshell
  - Let's get a reverseshell from pentestmonkey

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/13c26804-f788-4ff7-9340-b6ad176d5207)

  - After putting in our reverseshell we opened a netcat listener and got a shell!

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/a284fc3e-44d8-40bf-906a-7c53bb9cb9cc)

  - We can't open the key but we can open the password hash, looks like we need to do some cracking

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/cf3adea0-8739-49fe-a085-bb2a64dd8e75)

  - Hash identifier tells us this is an MD5 hash

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/aeb97d00-7a26-4d5a-a1b8-3979d8475412)

  - We got a password!

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/154d3731-23ba-4077-9960-7e5be3e86d86)

  - We can upgrade our shell to use su commands because they cannot be used in non interactive shells

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/4ff4ceab-6a5b-4d6a-bf48-af928bc1bf67)

  - now that we are robot we got the 2nd key

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/884f89f8-75a0-453e-8442-3d8b939730d9)

  - That nmap binary looks suspicious

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/d76f1412-a644-45e2-b562-3ad64ef0691b)

![image](https://github.com/JordanPenaloza/TryHackMe/assets/113396128/1e2d494c-4af3-4d62-8a7c-1e5561a35f09)

  - I looked up on gtfobins and looks like we can spawn an interactive shell by using nmap
  - root obtained!



