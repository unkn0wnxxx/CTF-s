# CTF Writeup: TeamCity Exploitation

---

Step 1: Enumeration --> nmap scan --> which ports are open?  
Step 2: Accessing page on ports found :80 & :50000  
Step 3: Port :80 displays maintenance page, while port :50000 prompts u to a login.html page  
Step 4: Version of TeamCity is outdated, googled for an exploit and found one  
Step 5: Used the exploit to login into the teamcity server.  
Step 6: ls /home --> found ubuntu dir --> ls /home/ubuntu --> found flag.txt and config --> cat /home/ubuntu/flag.txt  
Step 7: Started machine and logged into Splunk environment  
Step 8: filtered "All time" in searchbar and used command "source="/var/logs/auth.log" *install* to find the name of the backdoor user  
Step 9: used command "source="/var/logs/dpkg.log" date_month="july" date_mday="4" *package* to find it.  
Step 10: used command "source="/opt/teamcity/TeamCity/logs/teamcity-activities.log" *plugin* to find the name of the plugin installed after the exploitation.  

---

## Key Learnings

### - Learned about CVE's and increased my Git Knowledge
### - Increased my knowledge in navigating through reverse shells
### - First Learnings with Logs & Logfiltering via Splunk
