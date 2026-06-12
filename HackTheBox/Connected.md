+ Ports 22, 80, and 443 are open.
	+ 22 is an ssh service with version 7.4
	+ 80 is an http service that is running versions Apache 2.4.6, OpenSSL 1.0.2k-fips, and PHP 7.4.16
	+ port 443 is an https service with versions the same as above. 
+ Port 80 and 443 needs to be resolved to connected.htb in order to be accessed. 
	+ added the domain name 'connected.htb' to the /etc/hosts file. 
	+ entering the connected.htb provides me with what looks like a user control panel that runs on freePBX. Interestingly, the version it runs on is 16.0.40.7, which after looking it up online there are CVEs for versions 15, 16, and 17. The CVE that caught my eye was [CVE-2025-57819](https://nvd.nist.gov/vuln/detail/CVE-2025-57819). What this does is that any user-supplied data in api endpoints is unsanitized, which leads to arbitrary database manipulation and RCE (remote code exectution).
		+ There is a python [script](https://github.com/watchtowrlabs/watchTowr-vs-FreePBX-CVE-2025-57819/tree/main) that takes advantage of this vulnerability, which can be used to get a reverse shell started.
+ After using the python script for CVE-2025-57819, I used it to get a reverse shell started. 
	+ I used [Penelope](https://github.com/brightio/penelope#sample-typical-usage) to listen for the reverse shell and ran ```cat /etc/passwd```
+ Before starting any privesc techniques, I grabbed the flag from Asterisk's home directory. 
+ From there, I enumerate 