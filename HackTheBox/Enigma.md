
|    Name    |   Enigma   |
| :--------: | :--------: |
| Difficulty |    Easy    |
|    Site    | HackTheBox |
|    Type    |   Linux    |
# Enumeration

Scanning the IP address turned up with a ton of ports, but I focused on port 80 for now. It's an HTTP port that is running nginx 1.24.0 which has a custom DNS that needs to be resolved, so I added it in the hosts file. Once that was done, I looked into the site that was given. 

## Website - port 80

The site is a generic IT consultation website that offers services to corporations. I used [FFUF](https://github.com/ffuf/ffuf) to look for any directories that would be of interest. While I was enumerating for directories, I looked into the source page to look for any hidden comments or directories that could lead to anything I can use. The search was unsuccessful. I then inspected the network activity, headers, and the debugger just to make sure I didn't leave anything unchecked. Fuzzing for directories also turned up unsuccessful, so I decided to check for any subdomains. Again, unsuccessful. I decided to set my sights to other services in hopes of finding something. 

## POP3 -  port 110/995

Next on the list of opened ports is port 110, a service to retrieve emails from a remote mail server. 
