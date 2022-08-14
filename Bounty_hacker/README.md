This is a writeup for the [Bounty Hacker](https://tryhackme.com/room/cowboyhacker) practice room at tryhackme. Let's start hacking...

First, let's fire up the machine attached with the room. Now, let's set our IP variable to the IP address of the machine. This way we can now use IP variable and we donot have to write the IP address of the machine again and again. Command to set IP variable is:

```bash
export IP = 10.10.86.180
```
First and second question need no answers so let us move to third question.

**Answer 1: No answer needed**

**Answer 2: No answer needed**

Now, let us run the nmap scan by the following command:

```bash
sudo nmap -sV -sC -v -p- -O $IP
```
Flags used in the above command:
Flags      | Description
-----------|------------
-sV        |determine service/version info
-sC        |runs default nmap scripts
-p-        |for scanning all ports
-v         |Increase verbosity level
-O         |Enable OS detection

In the scan results we can see three ports are open.

![nmap](https://github.com/Kartik-Dixit/THM/blob/main/Bounty_hacker/images/nmap.png)
Port       | Service
-----------|------------
21         |FTP
22         |SSH
80         |HTTP

Now, as we know that a web server is running on port 80. So, let us try to access it from our browser. We will see a web page when we access the IP from our browser. While navigating on the web page we can't find somthing interesting. So, let's come back to our nmap scan.

![nmap_script](https://github.com/Kartik-Dixit/THM/blob/main/Bounty_hacker/images/script.png)

We can find something interesting in our nmap scan and that is **Anonymous FTP login allowed**. Let's try to connect to ftp with the user name anonymous:
```bash
ftp $IP
```

We are able to see two files on ftp server [locks.txt](https://github.com/Kartik-Dixit/THM/blob/main/Bounty_hacker/files/locks.txt) and [task.txt](https://github.com/Kartik-Dixit/THM/blob/main/Bounty_hacker/files/task.txt). So let's copy these files to our system by using mget command.
```bash
ftp> mget *
```
![ftp](https://github.com/Kartik-Dixit/THM/blob/main/Bounty_hacker/images/ftp.png)

Now let's view the content of the file. We will get the answer of third question in the task.txt file.

**Answer 3: lin**

When we look at the locks.txt file. It looks like a wordlist. From the nmap scan we know that port 22 is open and it's running SSH. As we already got a username "lin" and a wordlist that is "locks.txt", so let's try to bruteforce ssh using hydra.

**Answer 4: SSH**

Hydra command:
```bash
hydra -l lin -P locks.txt $IP ssh
```
Flags      | Description
-----------|------------
-l         |specify the username
-P         |specify the file containing passwords

We got the password!

**Answer 5: password you get through bruteforce**

Now we have the username and password, so let's login and connect to the target through SSH. 
```bash
ssh lin@$IP
```
We got the shell!

![ftp](https://github.com/Kartik-Dixit/THM/blob/main/Bounty_hacker/images/ssh.png)

We see a file user.txt in the home directory of lin. Let's display the content of this file and we got the user flag!

**Answer 6: content of user.txt file**

Now we have to look for privilage escalation for finding the root flag. So, let's run the following command:
```bash
sudo -l
```
This command will ask for password, so let us give the password of user "lin" which we already have.

Great, here we are seeing that user "lin" can run **tar** command as root. So let us look for privilage escalation using **tar** command on [gtfobins](https://gtfobins.github.io/gtfobins/tar/#sudo). Now let's run the tar command as shown [here](https://gtfobins.github.io/gtfobins/tar/#sudo) for privilage escalation. 

We got the root shell. So, now just display the content of the `/root/root.txt` file. We got the root flag!

**Answer 7: content of root.txt file**

Hurray! We completed the room!
