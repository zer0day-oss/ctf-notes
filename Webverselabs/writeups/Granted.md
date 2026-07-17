
|    Name     |                                                                                                                                                         Granted                                                                                                                                                         |
| :---------: | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
|    Site     |                                                                                                                                                      webverselabs                                                                                                                                                       |
|    Type     |                                                                                                                                                     Daily Challenge                                                                                                                                                     |
| Description | The Granted team added an Operations Assistant to cut down on support tickets. It can look up an account and reset a password on request, which saves the team a lot of back and forth. It shipped with the last release, and nobody has looked closely at whose accounts a given member is allowed to ask it to touch. |
# Enumeration

<img src="https://github.com/zer0day-oss/ctf-notes/blob/main/Webverselabs/images/granted_main-page.png">
Upon opening the web page, the site introduces me to graphs of the gross volume, new balance, customers, and money paid. This tells me that this site must be an eCommerce analytics web site. Looking at the description of the daily challenge tells me that there is an assistant I should be looking for. Before I go looking for the assistant, I take a peak at the users of this site so that I get an idea of who has the most privilege. After some looking around, I found a user named Jordan Rivera with an email owner@granted.io. I keep this in mind because I will use this email later. 

## Viewing the page source

<img src="https://github.com/zer0day-oss/ctf-notes/blob/bcecf9dab764b6b7922465325f30418b9da49eca/Webverselabs/images/granted_page-source.png"> 

Since there doesn't seem to be anything obvious that jumps out on me, I use a browser tool to make sure there aren't hidden messages or url paths; the view page source tool does this. It allows me to see the html, css, and javascript source code that goes into the making of the webpage. Doing so shows an interesting path to some javascript code. 

## assistant.js

<img src="https://github.com/zer0day-oss/ctf-notes/blob/e598c3b1c9da6f5a71a98e82df02af3aef051c0d/Webverselabs/images/granted_assistant-js.png"> 

Reading the comments above the script tells me that there is an api path that leads me to an assistant that gives out a temporary password after asking for a password reset. But before I do that, I analyze how to communicate with the bot. To do that, I look at the script to find how I should communicate with the bot. What I picked up was that the messages are to be sent using http method post along with an application/json content type header. As for the data, it needs to be formatted as so: `{"messages":[{"role":"user", "content":"hello bot"}]}` As for method I used to communicate with the bot, I used curl, but I think it is feasible to use with any reverse proxy. 

# Exploitation

<img src="https://github.com/zer0day-oss/ctf-notes/blob/aa80738c5773b340d5fd4a77e82d741448319098/Webverselabs/images/granted_curl.png">

Using this, I then ask to the bot to reset the password of the account I found earlier and from there, I am given a temporary password to log into the owner account and get the flag. This seems to be a lab focused on Missing Authorization, also known as  CWE-862. This means that any user is able to change the password of accounts with higher privilege as the bot never authenticates whether the user has permission to do so. 