
|    Name     |                                                                                                                                                         Granted                                                                                                                                                         |
| :---------: | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
|    Site     |                                                                                                                                                      webverselabs                                                                                                                                                       |
|    Type     |                                                                                                                                                     Daily Challenge                                                                                                                                                     |
| Description | The Granted team added an Operations Assistant to cut down on support tickets. It can look up an account and reset a password on request, which saves the team a lot of back and forth. It shipped with the last release, and nobody has looked closely at whose accounts a given member is allowed to ask it to touch. |
# Enumeration

<img src="https://github.com/zer0day-oss/ctf-notes/blob/main/Webverselabs/images/granted_main-page.png">
Upon opening the web page, the site introduces me to graphs of the gross volume, new balance, customers, and money paid. This tells me that this site must be an eCommerce analytics web site. Looking at the description of the daily challenge gives me an idea on what I should be looking for. 
## Viewing the page source
<img src="https://github.com/zer0day-oss/ctf-notes/blob/bcecf9dab764b6b7922465325f30418b9da49eca/Webverselabs/images/granted_page-source.png"> 
Since there doesn't seem to be anything obvious that jumps out on me, I use a browser tool to make sure there aren't hidden messages or url paths; the view page source tool does this. It allows me to see the html, css, and javascript source code that goes into the making of the webpage. Doing so shows an interesting path to some javascript code. 

<img src="