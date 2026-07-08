
|    Name    |   Nimbus   |
| :--------: | :--------: |
| Difficulty |    Hard    |
|    Site    | HackTheBox |
|    Type    |   Linux    |


# Enumeration

I used a [portscanner](https://github.com/zer0day-oss/portscanner.git) scan for open ports and found an ssh service that uses version OpenSSH 9.6p1, which seem to have a [CVE](https://nvd.nist.gov/vuln/detail/CVE-2025-26465) for this particular version, but I ignored this for now as there is another service that caught my attention. That service being an HTTP service on port 80 running nginx version 1.24.0 with no vulnerabilities that jump out at me. 
## Nimbus.htb

Checking the HTTP server, however, does reveal a few things. Namely, that checking the healthcheck link directs to a JSON page that reveal a AWS subdomain, which I added to my hosts file. I also fuzzed for directories and subdomains, which turned up with nothing. That leaves me with only an AWS subdomain and the /jobs directory that has something that looks like it takes .yaml inputs and parses it into some sort of job. 



