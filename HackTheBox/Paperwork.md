
| Name | Paperwork              |
| ---- | ---------------------- |
| Site | hackthebox             |
| Type | Season 11 Easy Machine |
| OS   | Linux                  |
# Enumeration

For starters, I scanned for ports, which got me ports 22, 80, and 1515. There are the usual ssh and http services, but there is also another port: 1515. 

## Ports

I looked port 1515 up to see which services usually run on this port and found out from the results that it's a port reserved for the ifor-protocol, which is used in local file transfers. Unlike ftp or sftp, it's a niche protocol that corporate systems or legacy applications. The applications in question aren't well-known so I assume that it's likely part of a custom or propriety system. However, what caught my eye is that if this port is exposed to the public internet, it lacks widespread adoption and documented security analysis, making it vulnerable to potential risks if misconfigured. The risks in question would be unauthorized file transfers or leaking of sensitive information. 
Port 22 runs an ssh server with the latest version. I didn't pay much mind to this as the focus wouldn't be on that. 
Port 80 runs an http server, where it hosts a corporate archive and records. In the site page, there is a link where you can download an archive. On that link is a version number of something called paperwork archive. Looking it up doesn't show anything relevant so I move on. 

## Fuzzing for subdomains and directories

I fuzzed the website for subdomains and directories. Using FFUF, I couldn't find any subdomains or directories. 

## Downloadable file







