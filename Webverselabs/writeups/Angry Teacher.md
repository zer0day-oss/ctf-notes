
|    Name     |                                                                                                                                                      Angry Teacher                                                                                                                                                      |
| :---------: | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
|    Site     |                                                                                                                                                      webverselabs                                                                                                                                                       |
|    Type     |                                                                                                                                                        Easy Lab                                                                                                                                                         |
| Description | South Park Elementary's grading portal is held together by a single developer's bad day. You log in as one of Mr. Garrison's struggling students, see all your failing grades, and somewhere on the page is a thread to pull. The teacher's API key is around here somewhere; once you find it, the rest writes itself. |
# Enumeration

Before I scan for open ports, I first read the description for the lab so that I gain an understanding with that I'll be working with and what I should primarily focus on; in this case, my goal is to find the API key. An API key is like a security badge that you use to enter restricted areas. In this case, though, we use an API key to gain access to the API (Application Programming Interface). In regards to this lab, the objective is to use the API key to change our grades. 

## Finding the API key

