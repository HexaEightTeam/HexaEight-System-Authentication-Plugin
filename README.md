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
4. Determine the Resource name for the Linux System and create a Resource Identity Token using your Email Address from HexaEight Mobile App. The Resource Identity is nothing but the machinename associated with this system that is used by the Token Server to identify this system. You can create a Generic Resource Name or a Domain Resource Name to associate with the system using HexaEight Mobile App. Once the QR Code is authorized using the Resource Identity Token, you will be prompted for an API Key
5. Enter the RAPID API Key. [Get An API Key Using This Link](https://rapidapi.com/hexaeight-hexaeight-default/api/hexaeight-sso-platform/pricing)

This above should complete the inital configuration. Now run the below commands to point to your Token Server and finally secure your installation
```
./HexaEight_PAM_Session --tokenserverurl
./setperm.sh
```
---
Add the below line to /etc/pam.d/sshd (assuming you already have sshd configured on your system)
```
auth       sufficient   pam_exec.so expose_authtok quiet /root/pam_x64/HexaEight_PAM_Session
```
finally create the email users in the system using the useradd command. Assign a random password to secure the user login

```
useradd john.doe--gmail.com
passwd john.doe--gmail.com (Assign a random password just to enhance the security of user. This password wont be used/needed)
```
---

On the HexaEight Token Server, use a wildcard setting or add entrires for all the email addresses you wish to authenticate on your system in the resourcepolicy.csv file like shown below

```
# ---------------System Authentication Policy------------------------
#   EMAILUSER |  DEST-HOST | AUTHSERVER | PERMISSION                            
# -------------------------------------------------------------------           
# p, /*@/mydomain.com, myunix.serverhost, mytoken.server, systemlogin            
# p, john.doe@gmail.com, mygenericid, mytoken.server, systemlogin
# -------------------------------------------------------------------  
```

### Testing

**Note : It is not possible to impersonate another email address even for testing purposes, as such you can only test using your email address.**

If you want to test the authentication, follow the below steps 
1. Create a Captcha Token on HexaEight Mobile App and point to your Token Server. Use the Captcha Token to generate a new Captcha on your Mobile.
2. Run the below steps as ROOT like shown below (this assumes you are John Doe and need to test authentication).
3. At the prompt type the captcha code, if the verification is successful, you can attempt to open a sshsession and login using another captcha code.
```
[root@localhost bin]# cd ~
[root@localhost bin]# export PAM_USER=john.doe--gmail.com
[root@localhost bin]# ./HexaEight_PAM_Session
Current Resource Owner:A9CB8EFAF7D258CC03DCD71C37295B5FE7BE435DF13A43239D34EEDD4C21D464
----------------------
Note: Ensure to verify the permissions of the current Directory
 and remove everyone except Service owner for Security purposes.
All OK. Press any key to terminate the program.
5Go7g
User Verified Successfully
[root@localhost bin]#
```



