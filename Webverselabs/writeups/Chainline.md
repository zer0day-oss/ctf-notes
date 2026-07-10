
|    Name     |                                                                                                                                                                              Chainline                                                                                                                                                                               |
| :---------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
|    Site     |                                                                                                                                                                             webverselabs                                                                                                                                                                             |
|    Type     |                                                                                                                                                                           Daily Challenge                                                                                                                                                                            |
| Description | The club outgrew its spreadsheet, so one of the members built a proper tracker over a couple of winters. The part everyone loves is import. Drop in the file your head unit saved and the whole ride appears, mapped and broken down by the kilometre. Whoever wrote it reckoned a file off your own device was safe enough to trust. It has not been touched since. |
# Enumeration

<img src="https://github.com/zer0day-oss/ctf-notes/blob/main/Webverselabs/images/Screenshot%202026-07-09%20at%2018-06-00%20Chainline%20%E2%80%94%20Log%20the%20ride.%20Own%20the%20climb.png?raw=true" alt="Image failed to load">

Opening the challenge, the website I was directed to looks like an ordinary online tracker with blog-like qualities. On investigation, however, I found the 'import ride' button located on the top-right corner of the site directs you to a file upload page, which an account is needed. I created a simple account and immediately went to the page responsible for uploading files. The files that can only be uploaded are gpx files, which are files that contain GPS data in XML format. I searched for any vulnerabilities regarding gpx files and came up with varied results and requisites that don't fit the server shown. I then redirected my attention to the XML format part and searched for that. I came up with results pointing to XXE (XML External Entity) vulnerabilities. 

# Vulnerability

Before making a gpx file with an XXE payload, I needed to test if the site is vulnerable to this type of attack, which means making a regular gpx file just to see what the response looks like. Luckily, the site already provides a sample gpx file to mess around with. I downloaded the file and uploaded it to see what it looks like. 

<img src="https://github.com/zer0day-oss/ctf-notes/blob/main/Webverselabs/images/Screenshot%202026-07-09%20at%2018-40-09%20Saturday%20Club%20Loop%20%E2%80%94%20Chainline.png?raw=true" alt="Image failed to load">

Now to see if it is vulnerable to a XXE injection. By adding `<!DOCTYPE replace [<!ENTITY foo "test"> ]>` to the line under the XML version and then replacing the text in the `<desc>&foo;</desc>` with this one. After uploading my edit, I got this:

<img src="https://github.com/zer0day-oss/ctf-notes/blob/main/Webverselabs/images/Screenshot%202026-07-09%20at%2018-55-58%20Saturday%20Club%20Loop%20%E2%80%94%20Chainline.png?raw=true">
This confirmed that the site is vulnerable to XXE and I can then exploit the site to give me the flag. 

# Exploitation

After some trial and error, (the errors in which case was trying to find the flag, which if not found or the file is not present, there will be an error message instead of the file being uploaded - HANDY!), I found the flag in the '/' directory instead of the rider home directory found in '/etc/passwd'. The injection sample I used to get it was `<!DOCTYPE data [<!ENTITY foo SYSTEM "file:///foo/bar"> ]>` (replace 'foo/bar' with the file in question) and I got the flag! Good luck hackers! 






