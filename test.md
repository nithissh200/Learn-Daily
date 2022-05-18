# Interesting XSS by changing the username of my Instagram account 
Hi people, I hope you are doing great and being healthy. Few days back , I was working on a target where I found an Interesting stored XSS with a link account functionality in the target web application. 

## How the application works ?
- - - -
The application is based upon the medical e-commerce model where the application sells the medicinal products and medical stuffs. The application has multiple roles like shop owner , buyer and manager. The shop owner has separate panel for them to assess in generating the static web application in order to sell their products. The manager role has only two step process like the seller had created the static sites for their product to sell and the manager role people has to validate the products and do background check of seller in order to provide them a better platform to avoid people from getting scammed or to avoid getting cheated by the fake seller

## How I found this Vulnerability ?
- - - -
Initially I started looking around for vulnerability as a high privileged user like seller and manager looking around for IDORs , Broken access controls and authentication related but I didn’t had much success like literally nothing. But I questioned myself  ==There is File upload functionality out there I can able to upload any type of files but image loads up in blob storage and doesn’t execute.==. Later on I started looking around as a normal user where I found there is functionality in this application where we can able to link around 5 to 7 third party applications like Facebook,twitter, LinkedIn, Instagram, etc. 

So , I started looking for some simpler vulnerabilities like tabnabbing and whether we can link to a social media account by overwriting with same mail address of what we used it for the registration purpose ?==. I always look for something stupid but it ends up being weird vulnerability. 

> **What’s next ?** , Originally when the application links a third party application. The application will render the thirty party application username in the target application.  

So , Everyone’s spider sense got triggered haha you guys have found **what the issue will be ?** . Absolutely yes , let’s discuss further

{{ Spider-Man Tingling GIF }}

## How I exploited this Vulnerability ?
- - - -
* As previously said , when the user links a third party account for example , I’m gonna link my Instagram account on to the current application . Once the link between the current application and third party applicant is done. The application will now reflect the User name of the third party applicant on to the current application 

> For Instances , If my Instagram username is nithissh and I linked the Instagram account on to my current application . Now while viewing the profile the application will reflect my Instagram username in the application user profile  

* Now , whenever the text got reflected in the response page we will be always thinking off to test for XSS. So, I came up with a idea of changing my instagram username to a XSS payload and I tried linking the instagram once again 

> To be clear , My current Instagram username is nithissh So, I changed the username from **nithissh** to **<img src=a onerror=alert(document.domain)>** and let’s check what really happens  

* After changing the username of my Instagram account to an XSS payload and after linking the account to my current application and To my surprise , it works application executed the code and the XSS will get triggered 

> **What’s the thought process here ?** , Everyone will have the idea right ? , whenever the application reflects the value or text on to the response page . Always check the source code where it got reflected ? . Is it getting sanitized ? If not try for a XSS . It will definitely works don’t rely on the bypass payloads xD   

## Conclusion
This vulnerability also affects other users , admin , sellers and managers like a site-wide stored XSS . The funny part is even it got fired in the internal admin panel. The vulnerability is kind of weird and interesting for me if you guys have previously known about this vulnerability that’s Great
