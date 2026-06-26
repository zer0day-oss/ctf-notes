
|    Name    |   Nimbus   |
| :--------: | :--------: |
| Difficulty |    Hard    |
|    Site    | HackTheBox |
|   Ports    | 22 and 80  |
#Enumeration
	I used a [portscanner](https://github.com/zer0day-oss/portscanner.git) scan for open ports and found an ssh service that uses version OpenSSH 9.6p1, which seem to have a [CVE](https://nvd.nist.gov/vuln/detail/CVE-2025-26465) for this particular version, but I ignored this for now as there is another service that caught my attention. That service being an HTTP service on port 80 running nginx version 1.24.0 with no vulnerabilities that jump out at me. 
	Checking the HTTP server, however, does reveal a few things. Namely, that checking the healthcheck link directs to a JSON page 
	

