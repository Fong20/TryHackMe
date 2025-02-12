# Blue
Summary of Blue room: Exploitation of Windows machine using MS17-010 Eternal Blue Exploit

## Recon phase
The room starts off by asking for the number of ports which are open with a port number of less than 1000. To find the answer, we use the following Nmap command to scan for available ports

![image](https://github.com/user-attachments/assets/fa197e7a-a273-4d6c-9e30-fd22d4fac375)

Next, the question prompts us to identify the vulnerability which the targeted machine is exposed to. To solve this question, we use the following nmap command, `nmap -sV --script vuln -v` followed by the ip address of the virtual machine.

**Nmap command breakdown:**
- `-sV` This scans for the versions of discovered services.
- `--script` Scripting Engine.
- `vuln` Investigate vulnerabilities or exploit vulnerable services.

![image](https://github.com/user-attachments/assets/de67172c-079c-4a00-b834-acaaa2fc7555)

The scan revealed that the targeted machine is vulnerable to the MS17-010 vulnerability

![image](https://github.com/user-attachments/assets/37a4416c-0196-4fb7-8042-bdfc99e7a14c)

## Gain access

## Escalate

## Cracking


## Finding flags
### Flag 1
Based on the question, it is stated that flag 1 can be found at the system root, which is C:

![image](https://github.com/user-attachments/assets/8295c184-c850-46ca-b423-1c578cadcfc2)

### Flag 2
Based on the question, it is stated that flag 2 can be found at the location where passwords are stored within Windows. Since lsass.exe is stored in the C:\Windows\system32 which manages user credentials, we can assume flag2.txt is placed somewhere in system32 directory.

We can then use the search command to look for the file

![image](https://github.com/user-attachments/assets/5982d8b7-1e4d-4346-a8b4-47550a6d9e6b)

Once we have identified the exact location of the file, we can then navigate to the exact path to obtain the flag

![image](https://github.com/user-attachments/assets/db5c3f59-414d-4740-8b97-46fc5a9477f9)


### Flag 3
Based on the question, flag 3 can be found in the location where things are usually stored by the adminstrator. In this case, it would be the user directory. 

Once we are in the Users directory, we can examine the Documents directory for the text file containing the flag, flag3.txt

![image](https://github.com/user-attachments/assets/dfbda33f-2493-457e-882c-a0ba52de167c)
