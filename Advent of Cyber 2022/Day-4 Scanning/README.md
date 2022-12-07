# The Story
During the investigation of the downloaded GitHub repo (OSINT task), elf Recon McRed identified a URL qa.santagift.shop that is probably used by all the elves with admin privileges to add or delete gifts on the Santa website. The website has been pulled down for maintenance, and now Recon McRed is scanning the server to see how it's been compromised. Can you help McRed scan the network and find the reason for the website compromise?

First let's start the machine attached with the task.
Now we can connect to the machine using either attackbox or openvpn.

Note: ***Change the target_ip with the machine IP.***

## Connect using openvpn 
First download your openvpn configuration file.
Now on your linux machine type
```bash
sudo openvpn config_file_path
```
Change the config_file_path with you configuration file path.

## Task 1: What is the name of the HTTP server running on the remote host?
Let's run the SYN scan using nmap.
```
sudo nmap -sS target_IP
``` 
We will see the server name that is running on port 80.

## Task 2: What is the name of the service running on port 22 on the QA server?
In the result of the above command you will see the service running on port 22.

## Task 3: What flag can you find after successfully accessing the Samba service?
So let's start doing some smb enumeration. First let's find the sharenames using smbclient.
```bash
smbclient -L target_IP
```
Leave the password field blank and hit enter.
We will see the list of sharenames. We can see that there is a admins share.
So let's try to look what is inside it using the credentials which are provided in the task.
Again we will use smbclient here
```bash
smbclient //target_IP/admins -U ubuntu
```
Password is: S@nta2022
Now we are inside the admin share. Let's list the content using ls.
We will see two files with the name flag.txt and userlist.txt.
So now let's get these files on our local computer. Type the following command
```bash
get flag.txt
```
and 
```bash
get userlist.txt
```
Now exit out of smbclient. And list the content of the flag file.
```bash
cat flag.txt
```
Just submit the flag.

## Task 4: What is the password for the username santahr?
While solving the above task we got a file with the name userlist. Just view the content of the file and we will get the password.  


