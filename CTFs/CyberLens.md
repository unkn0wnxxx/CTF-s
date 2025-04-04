# CTF Writeup: CyberLens

---

Step 1: Checked out websited and checked out functionalities, 
--> /images directory, fileInput script found in source code --> potential script vulnerability,
contact us input fields --> maybe html injection vulnerability.
- Step 2: checking some sub dir's, /robots.txt, /images
- Step 3: analyzed all images in /images --> found same picture in .jpg and .webp format, suspicious
- Step 4: Enumeration --> "nmap -A <target_ip>" --> port 80 running on outdated apache server 2.4.57,
port 135 is open asw -> Microsoft windows rpc, port 139 is open --> ms windows netbios-ssn, 
445 is open microsoft-ds? and port 3389 --> microsoft terminal servies
- Step 5: Continued with enumeration, because I couldn't find any important clues, looked into the script
and found another dir and added it into /etc/hosts to bypass DNS
- Step 6: Got access to the website, but doesn't display anything. Tried to intercept traffic with proxy
burpsuite, forwarded the request and captured it within my repeater, but no result asw and no manipulation poss.
- Step 7: Looking for hidden dir's in the newly found web server on port 61777 
--> gobuster dir -u http://10.10.27.101:61777 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
--> Found new hidden dir "/version" and found out that the server is ran on apache tika 1.17
- Step 8: made msfconsole -q to open up metasploit and made "search apache tika 1.17" and found CVE
- Step 9: made "use 0", configured RHOSTS, RPORT and LHOST and made "exploit" 
- Step 10: Gained reverse shell inside the windows server 
- Step 11: went to / --> went to Users --> Went to CyberLens --> Went to Desktop --> found user flag
- Step 12: Can't access "Administrator" dir, so need to do privilege escalation --> using winPEAS to get results.
- Step 13: Ran WinPEAS and it found privilege escalation "alwaysinstalledelevated", because HKLM and HKCU is
set to 1 on the windows server.
- Step 14: restarted metasploit & made background to apache tika exploit, made "search alwaysinstalledelevated"
--> configurated it properly and made "run", made "getuid" to find rights and we are administrator --> went to
administrator dir and found admin.txt --> root flag


---

## Key Learnings

- Increased Metasploit Knowledge
- Increased Enumeration Skills
- Increased Windows CLI Knowledge
- Increased Privelege Escalation Knowledge
- Gained Knowledge about WinPEAS

