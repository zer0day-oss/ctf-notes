
|    Name     |                                                                                                                                                      Angry Teacher                                                                                                                                                      |
| :---------: | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
|    Site     |                                                                                                                                                      webverselabs                                                                                                                                                       |
|    Type     |                                                                                                                                                        Easy Lab                                                                                                                                                         |
| Description | South Park Elementary's grading portal is held together by a single developer's bad day. You log in as one of Mr. Garrison's struggling students, see all your failing grades, and somewhere on the page is a thread to pull. The teacher's API key is around here somewhere; once you find it, the rest writes itself. |
# Enumeration

Before I scan for open ports, I first read the description for the lab so that I gain an understanding with that I'll be working with and what I should primarily focus on; in this case, my goal is to find the API key. An API key is like a security badge that you use to enter restricted areas. In this case, though, we use an API key to gain access to the API (Application Programming Interface). In regards to this lab, the objective is to use the API key to change our grades. 

## Finding the API key

Now that I know what the objective of this lab is, I will need to find the API key. I started with viewing the source page of the website since there are times that web developers will hide clues, comments, credentials, and/or scripts. I didn't need to look any further than that because the API key was hidden in the html comments. 

<img src="https://github.com/zer0day-oss/ctf-notes/blob/949f38bfb063d89382d123b52b89ed4a4bf6549b/Webverselabs/images/angryteacher_pagesource.png" alt="page source of the website">

With the API key, I now have access to the API, which would allow me to change the grades. In fact, before I viewed the page source, there was a comment in red that mentioned that the grades has to be above 70+ or his parents would be called. This gives me a clue to what values need to be changed. Unfortunately, the values to be changed are not found in the main page, meaning that there is a separate directory that this is found in. Additionally, the page source doesn't even show the grades there. However, this is a clue in itself because that means the information is being pulled from elsewhere. After all, every contact leaves a trace! In the case of web penetration, to view this trace is to use the browser developer tools, namely the Network tab to find who this site contacts to pull that resource, and voilà. The directory it pulls the resource from is /api/grades/1/1. The last part being the subject id. Before I did anything though, I directly checked what http methods I am allowed to use on that API by sending the http OPTION method through curl, which sent back `Access-Control-Allow-Methods: GET,HEAD,PUT,PATCH,POST,DELETE`. Good, that means I can use every method as long as I have the API key, which the header to use for such a key is the `Authorization: <API-KEY>` header. 

# Exploitation

To change the grades, I would need to know how the the resource is pulled. Luckily, viewing the network tab again, and looking at the response of the url mentioned above, shows that the data is in json format. Namely, `{"id":<int>,"student_id":<int>,"subject":<str>,"grade":<int>,"comment":<str>}`, and because it's in json format, I need to explicitly mention in the Content-Type header that it is 'application/json' so that it reads it right. With all this known, it's time to change the grades. Initially, I used the PATCH http method, but that produced an error. I later found out that the PUT method is the way to go.  

<img src="https://github.com/zer0day-oss/ctf-notes/blob/8a0d9fcf36e42efd434444662c653277e924e7e2/Webverselabs/images/angryteacher_curl.png" alt="image of the curl command"> 

After doing this for all four subjects, I got a flag on the fourth subject through the main page used to view the grades. This type of attack is a classic IDOR (Insecure Direct Object Reference) vulnerability.  

