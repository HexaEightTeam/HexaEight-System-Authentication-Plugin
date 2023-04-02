# HexaEight-System-Authentication-Plugin

Implement HexaEight Authentication in Linux, Raspberry Pi, Windows, Mac and even custom Operating Systems

Getting Started:

HexaEight Systen Authentication Plugin uses PAM authentication for authenticating email users in all flavour of Linux (x64 version) and Raspberry pi devices (arm_64 version).  The authentication plugins for Windows and Mac will be updated once its ready.

**Note : Linux Operating Systems cannot have @ as part of the username, as such, it is not possible to input email address in the username. Hence HexaEight PAM module replaces @ with a -- (doublehash) when mapping email address to linux usernames**

For Example : If your email address is john.doe@gmail.com, your linux login username is automatically mapped to john.doe--gmail.com by HexaEight PAM module.

Download Links

[Linux X64 - Most Flavour of Linux](https://www.hexaeight.com/downloads/HexaiEght_System_Authentication_Plugins/pam_x64.zip) 

[ARM X64  - Raspberry pi Version](https://www.hexaeight.com/downloads/HexaiEght_System_Authentication_Plugins/pam_arm64.zip) 

Follow the instructions to install and activate HexaEight PAM module in the system.

1. You need to have ROOT priviliges to install HexaEight PAM Module.
2. Use wget or curl to download the PAM module zip 
```
wget https://www.hexaeight.com/downloads/HexaiEght_System_Authentication_Plugins/pam_x64.zip
cd ~
unzip pam_x64.zip
```
3. The above command will create a folder called pam_x64 in the root directory. Run the below commands to set appropriate permissions to all the files in the pam_64 folder and generate a machine code for the PAM module.
```
cd ~
chmod 700 pam_64
cd pam_x64
chmod 700 setperm.sh
./setperm.sh
./HexaEight_PAM_Session --generatemachinecode
```
4. lsdldsds
5. 


