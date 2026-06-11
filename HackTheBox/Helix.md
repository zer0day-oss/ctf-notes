+ Started with port scan and then enumerated with nmap scan. 
	+ ports 22 and 80 are open. 
+ webpage on port 80
	+ page source of webpage doesn't show anything interesting interesting. 
	+ no interesting directories was found using ffuf. 
	+ using ffuf for scanning subdirectories revealed a subdirectory named flow. 
		+ going to http://flow.helix.htb/ revealed a redirect to the /nifi directory.
		+ this directory reveals that it uses Apache Nifi, a database framework that focuses on automating data pipelines and distribution. It uses version 1.21.0.
			+ This version has a critical vulnerability, [CVE-2023-34468](https://nvd.nist.gov/vuln/detail/CVE-2023-34468), which allows an authenticated user to configure a Database URL with the H2 driver that enables custom code execution. 
				+ There is a [PoC](https://github.com/mbadanoiu/CVE-2023-34468/blob/main/Apache%20NiFi%20-%20CVE-2023-34468.pdf)that explains this vulnerability and exploit in detail. 

