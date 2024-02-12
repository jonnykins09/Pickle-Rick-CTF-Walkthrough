# Pickle Rick CTF Walkthrough

![Untitled](Pickle%20Rick%20CTF%20Walkthrough%20e8ab250892b14005a653d7deaaffa763/Untitled.png)

Today, we’re going to run through the Pickle Rick CTF and see if we can find all the ingredients to change Rick back into a human. 

![Untitled](Pickle%20Rick%20CTF%20Walkthrough%20e8ab250892b14005a653d7deaaffa763/Untitled%201.png)

First, let’s deploy the machine to obtain an IP on the target. 

![Untitled](Pickle%20Rick%20CTF%20Walkthrough%20e8ab250892b14005a653d7deaaffa763/Untitled%202.png)

Starting out, I’m going to do a quick Nmap scan to see what ports are open, and check service versions on the target. I’ll do this with Nmap -sV 10.10.165.37.

![Untitled](Pickle%20Rick%20CTF%20Walkthrough%20e8ab250892b14005a653d7deaaffa763/Untitled%203.png)

Port 22 (SSH) and port 80 (HTTP) are open, and the target is running Linux. Let’s see what we find on the insecure protocol http. Going to the web browser, I enter http://10.10.165.37:80.

![Untitled](Pickle%20Rick%20CTF%20Walkthrough%20e8ab250892b14005a653d7deaaffa763/Untitled%204.png)

Rick wants us to log in to his computer to get the ingredients, but he cant remember his password. Let’s see if we can find it. I’m going to run Gobuster against a directory wordlist, and Nikto to find any vulnerabilities. While they’re running, I’m going to check the page source code.

![Untitled](Pickle%20Rick%20CTF%20Walkthrough%20e8ab250892b14005a653d7deaaffa763/Untitled%205.png)

We found a username in the comments of the source code. Very sloppy Rick! Let’s make a note of that and see what Gobuster and Nikto find for us. **Username: R1ckRul3s**

![Untitled](Pickle%20Rick%20CTF%20Walkthrough%20e8ab250892b14005a653d7deaaffa763/Untitled%206.png)

We found a few directories, so lets see what they show us.

![Untitled](Pickle%20Rick%20CTF%20Walkthrough%20e8ab250892b14005a653d7deaaffa763/Untitled%207.png)

/assets doesn’t have anything out of the ordinary. I did check the pictures and gifs for stenography, but nothing was hidden there. Let’s move on.

![Untitled](Pickle%20Rick%20CTF%20Walkthrough%20e8ab250892b14005a653d7deaaffa763/Untitled%208.png)

/robots.txt is interesting, and I believe we may have found a password. Until we know for sure, I’m going to assume this is the password to the username we found earlier. ***Password: Wubbalubbadubdub.***

![Untitled](Pickle%20Rick%20CTF%20Walkthrough%20e8ab250892b14005a653d7deaaffa763/Untitled%209.png)

I tried to ssh into the box with the credentials, but without a ssh key, I’m not getting in. I’m a little stumped here as gobuster isn’t finding any other directories. Nikto is still running, so I’m going to walk away and wait for it to finish and see if it finds any clues.

![Untitled](Pickle%20Rick%20CTF%20Walkthrough%20e8ab250892b14005a653d7deaaffa763/Untitled%2010.png)

I scanned through the logs of Nikto while it was running, and saw a 200 for /login.php. Fingers crossed that this is what was overlooked!

![Untitled](Pickle%20Rick%20CTF%20Walkthrough%20e8ab250892b14005a653d7deaaffa763/Untitled%2011.png)

![Untitled](Pickle%20Rick%20CTF%20Walkthrough%20e8ab250892b14005a653d7deaaffa763/Untitled%2012.png)

![Untitled](Pickle%20Rick%20CTF%20Walkthrough%20e8ab250892b14005a653d7deaaffa763/Untitled%2013.png)

The username and password we found work in the login portal and we’re in! 

![Untitled](Pickle%20Rick%20CTF%20Walkthrough%20e8ab250892b14005a653d7deaaffa763/Untitled%2014.png)

ls shows us a list of items in out working directory, and it looks like we may see our flag. Lets cat it and see what it says

![Untitled](Pickle%20Rick%20CTF%20Walkthrough%20e8ab250892b14005a653d7deaaffa763/Untitled%2015.png)

Command disabled? It couldn’t be that easy. Nano also doesn’t work. Let’s try tac and see if we can read the file from the end.

![Untitled](Pickle%20Rick%20CTF%20Walkthrough%20e8ab250892b14005a653d7deaaffa763/Untitled%2016.png)

![Untitled](Pickle%20Rick%20CTF%20Walkthrough%20e8ab250892b14005a653d7deaaffa763/Untitled%2017.png)

It worked! Looks like our first flag is “mr. meeseek hair”. 

![Untitled](Pickle%20Rick%20CTF%20Walkthrough%20e8ab250892b14005a653d7deaaffa763/Untitled%2018.png)

Clue.txt says to look around the file system for another flag. After trying to work my way around the directory, I realized that it automatically went back to the same folder after the command was run. So I used “;ls -la” after my traversal to display the contents of the working directory after my traversal. 

![Untitled](Pickle%20Rick%20CTF%20Walkthrough%20e8ab250892b14005a653d7deaaffa763/Untitled%2019.png)

Great! Lets see what users are on this system.

![Untitled](Pickle%20Rick%20CTF%20Walkthrough%20e8ab250892b14005a653d7deaaffa763/Untitled%2020.png)

![Untitled](Pickle%20Rick%20CTF%20Walkthrough%20e8ab250892b14005a653d7deaaffa763/Untitled%2021.png)

We found the second flag! Make sure to put the file in quotations since it has a space in the name. After opening it and entering the answer into tryhackme, we have one more flag to go.

![Untitled](Pickle%20Rick%20CTF%20Walkthrough%20e8ab250892b14005a653d7deaaffa763/Untitled%2022.png)

![Untitled](Pickle%20Rick%20CTF%20Walkthrough%20e8ab250892b14005a653d7deaaffa763/Untitled%2023.png)

![Untitled](Pickle%20Rick%20CTF%20Walkthrough%20e8ab250892b14005a653d7deaaffa763/Untitled%2024.png)

Ideally, the last flag will be in the root folder, so lets hopefully make our way over there next. Does this user have sudo permissions so we can get into /root? YES. Let’s get into that root folder baby!

![Untitled](Pickle%20Rick%20CTF%20Walkthrough%20e8ab250892b14005a653d7deaaffa763/Untitled%2025.png)

We found the 3rd and final ingredient.

![Untitled](Pickle%20Rick%20CTF%20Walkthrough%20e8ab250892b14005a653d7deaaffa763/Untitled%2026.png)

![Untitled](Pickle%20Rick%20CTF%20Walkthrough%20e8ab250892b14005a653d7deaaffa763/Untitled%2027.png)

![Untitled](Pickle%20Rick%20CTF%20Walkthrough%20e8ab250892b14005a653d7deaaffa763/Untitled%2028.png)

Room completed!

# Conclusion:

Had it not been for Nikto, and being lucky looking through the logs, I wouldn’t have found the php login page easily. I couldn’t imagine what I would have gotten into had I not come across it. I found the room to be laid out well, and relatively easy (although I went down a rabbit hole looking for stenography in the website images).  See you on the next walkthrough!