# The Story
As the elves are trying to recover the compromised santagift.shop website, elf Recon McRed is trying to figure out how it was compromised in the first place. Can you help him in gathering open-source information against the website?  

## Task 1: What is the name of the Registrar for the domain santagift.shop?
Here we can use the whois command which is preinstalled in kali linux and parrot os.
```bash
whois santagift.shop
```
We can also use the [who.is](https://who.is/) website.
After getting the whois info. Just look the name of registrar in Registrar info.

## Task 2: Find the website's source code (repository) on github.com and open the file containing sensitive credentials. Can you find the flag?
1. Open github.com in your browser. 
2. Now in the search box let's search for "santagift.shop". 
3. We can see a repository with the name "SantaGiftShop".
4. When we will look in the repository we will see a files section in README.md. Here it is mentioned that credentials are stored in config.php. 
5. So, let's open config.php file. We can see the flag in the 2nd line.

## Task 3: What is the name of the QA server associated with the website?
We found a repository with the name "SantaGiftShop" in the previous task.
When we look config.php file. We will see in the 20th line, it is written that "Incase of QA, it will be qa.santagift.shop". 
So, we got the name of the QA server.

## Task 4: What is the DB_PASSWORD that is being reused between the QA and PROD environments?
Again let's look at the config.php file. We will see the DB password in 31th and 55th line.

