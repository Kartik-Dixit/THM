This is a writeup for the [Bounty Hacker](https://tryhackme.com/room/attackerkb) practice room at tryhackme. Let's start hacking...

First, let's fire up the machine attached with the room. Now, let's set our IP variable to the IP address of the machine. This way we can now use IP variable and we donot have to write the IP address of the machine again and again. Command to set IP variable is:

```bash
export IP = 10.10.86.180
```

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


