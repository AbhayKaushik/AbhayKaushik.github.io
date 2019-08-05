---
layout: post
title:  "Automating Image Scraping"
date:   2019-07-31 10:09:50 +0530
categories: jekyll update
---
Yeah, this is the second part of image scraping blog. You see, even after making the script, I was not satisfied.

First, I will have to execute the script every time I want to see the latest images (obviously..) but I may forget to run the script one morning (it’s really difficult to be regular :P)

Second, the sub-reddits that I have selected are very active and new posts keep popping up. 
So, it’s quite possible that I may lose some of them if I don’t check on them regularly.
Reddit only loads the top posts according to preference and you have to scroll down to load more, which makes it difficult to scrape the entire page and you only get these top posts.

Now, as you may have guessed, the answer to this : automation! So, I searched on how to automate scripts, and I stumbled across cron jobs.

Basically, cron is a time-based job scheduler in Unix-like computer operating systems. 
Cron is used to schedule jobs to run periodically at fixed times, dates, or intervals, especially by those maintaining software environments.

You can learn more from this [link][cron-link]

First I had thought of automating this process in a cloud VM, and host a site with periodically changing the html file stored there.
However, it is diffcult to do without a billing account (I am not going to use credit cards just yet :D )

I stumbled across many searches and methods and finally reached MongoDB along with Heroku. It may work but it'll take more time, so I will cover it in some other post.

Now, I will the run the script that I made earlier with some changes. Actually, I learnt later that you can access the rss feeds of a site by using .rss 
I tried wth .xml, but it doesn’t work everytime.
 
Turns out, their xml and rss equivalents don’t have img tags, instead they have a description or content tag with the image details, like this: 
```xml
<content type="html"> ... &lt;span&gt;&lt;a href=&quot;https://i.imgur.com/V139kHFds.jpg&quot;&gt;[link]&lt;/a&gt;&lt;/span&gt; &amp;#32; &lt;span&gt;&lt;a href=&quot;https://www.reddit.com/r/comics/comments/cm9ludw/&quot; ... </content>
```

This won’t work with my script. The turnoff link is an exception as it has the img tag. (I think these feeds are dependent upon the maintainers of these sites)

So, currently my script looks like this:

```python
#Import libraries
import requests
import urllib.request
import time
from bs4 import BeautifulSoup
import os

#Initial Things to Load each Time

#Last Link list loaded
check_list = []
with open('/home/abhayk/Documents/check.txt', 'r') as file:
    for row in file:
        check_list.append(row.split('\n')[0])
file.close()


#List to store the last links obtained from each site
last_link = []

#list to store the responses
response_list = []

current_time = int(time.localtime()[1])*100+int(time.localtime()[2])
#--Part 1: The Reddit Script--

response = requests.get('https://www.reddit.com/r/comics/')
tries = 0

#Make multiple requests to busy server 
while not response.ok and tries < 20:
    time.sleep(1)
    response = requests.get('https://www.reddit.com/r/comics/')
    tries += 1
    
print("Response recieved")
soup = BeautifulSoup(response.text, 'html.parser').findAll('img')
for i in range(len(soup)-1,-1,-1):
    tag = soup[i]
    link = tag['src']
    if 'external' in link or 'static' in link:
        continue
    n_link = link.split('?')[0].replace('preview','i')
    if not n_link in check_list:
        response_list.append((current_time, n_link))
    else:
        break
        
print("Part 1 successful")
if len(response_list) != 0:
    last_link.append(response_list[::-1][0][1])

#--Part 2 : The Everything Else Script--

#list of urls
url_list = [
    'https://turnoff.us/feed.xml',
    'http://www.incidentalcomics.com/',
    'https://xkcd.com/'
    ]

idx = 0
for url in url_list: 
    response = requests.get(url)

idx = 0
for url in url_list: 
    response = requests.get(url)
    if(response.ok):
        soup = BeautifulSoup(response.text, 'html.parser').findAll('img')
        tag = soup[idx]
        link = tag['src']
        if idx < 1:
            idx += 1
        if not link.startswith('h'):
            #Adding https in the start to create a valid link
            link = 'https:' + str(link)
        last_link.append(link)
        if not link in check_list:
            response_list.append((current_time,link))
            

#--Saving the last links to a file --

#We will overwrite the file and enter new contents
with open("/home/abhayk/Documents/check.txt",'w') as file:      
    for l in last_link:
        file.write(str(l) + "\n")

print("Checks Updated")
#Deleting file content older than 30 days

older_than_days = 30
#Check for older images and delete those links
if os.stat("/home/abhayk/Documents/response.txt").st_size != 0 :
    with open("/home/abhayk/Documents/response.txt",'r') as file:
        storage = file.readlines()
        #print("Storage:", storage)
    with open("/home/abhayk/Documents/response.txt",'w') as file:    
        for r in storage:
            if current_time - int(r.split(',')[0].strip('(')) <= older_than_days:
                file.write(r) #\n not added as previously added strings would already contain it
            
print("Response backlog deleted")
#Add the new responses to the file
with open("/home/abhayk/Documents/response.txt",'a') as file:      
    for r in response_list:
        #print("r in response list: ", r)
        file.write(str(r) + "\n")
        
#Overwrite the new file with the links now in response_list:
insert_list = []

if os.stat("/home/abhayk/Documents/response.txt").st_size != 0 :
    with open("/home/abhayk/Documents/response.txt",'r') as file:      
        for l in file:
            insert_list.append(l.split('\'')[1])


insert_list.reverse()
print("New response data added")
#Add the links to image tags in the html page        
with open('/home/abhayk/Documents/index.html','w') as page:
    open_tags = "<html>\n<head>Meme Page</head>\n<body>\n<p>Hey! This is a page for some blogs that feature meme content.</p>\n"
    css_code = "<style> img.resize{\nmax-width:50%;\nmax-height:50%;\n}\n </style>\n"
    image_tags = ""
    for link in insert_list:
        image_tags += "<div><img style = 'max-width:800px;' src = '" + link + "'></div>\n"
    end_tags = "</body>\n</html>"

    code = open_tags + css_code + image_tags +end_tags
    page.write(code)    

print("HTML updated")
```
Changes I made are:

- Added the libraries to the script (I was developing in a Jupyter, so I noticed it later :P)
- Reversed the response list (old blogs were coming up on top.)

    NOTE: I later realized that I was web scraping from the reddit page where posts were ordered according to their popularity, so it was bound to change. 
    The fix : shift to new sorting instead of the popularity sorting!
    ```python
    response = requests.get('https://www.reddit.com/r/comics/new/')
    ``` 
- Added absolute paths to the file instead of relative paths (better safe than sorry :D)
- Added os.stat condition so that I don't process an empty file

## Chronic Cron

Now, I had already seen crontab before learning about cloud schedulers, so I was wondering of I could write a cron job within my computer to excute the script. 

For that, I used crontab in my local computer. The only downside will be that the process will be skipped if my computer is not turned on. 
This is particularly not the case in my vacations but could be possible when my college starts (this was for free time anyways :P) 

So, first I tried a simple cron job of inserting text in an empty file :
```shell
20 17 * * * echo "This works" > /home/abhayk/Documents/img.txt 
```
And it works :D

I checked the syslog in /var/log/syslog and saw this among the lines:
```bash
$ grep CRON /var/log/syslog

CRON[1321]: (abhayk) CMD (echo "This works" > /home/abhayk/Documents/img.txt )
```
Now, I had to run a python script in my cron job.

First, make sure that your python script is executable.
```bash
chmod +x imagegrab.py
```
I was having some difficulties on how to handle python scripts as most of the examples were on bash scripts.

And then I found just the thing, [python-crontab][python-crontab-link]

I used this [blog][python-crontab-blog] to help setup my cron jobs using python-crontab

After all this, the only problem left was to make sure that my laptop has an internet connection.
Not entirely independent till now.

But it's an improvement. Atleast my script will run once a day in the morning (mostly without fail :P)

(Well the cron job is not working right now, so I will update the blog when I find a fix)

And here we are at the end of this blog. (Or are we? XD)

## Not Content Without Bonus Content

Now,I recently learnt to create an onion service in Tor and have added the html file created by script to it.
So, here’s the [link][onion-link] for the same if you want to see the images (it can only be accessed using tor browser though :P) 

It may not work always as it is self-hosted (currently), but it can be whatever I want. 

If you too want to make your own onion service (especially if you have a server lying around :P), you can see this [blog][blog-link]

[cron-link]: https://www.adminschoice.com/crontab-quick-reference
[python-crontab-link]:https://pypi.org/project/python-crontab/
[python-crontab-blog]:https://stackabuse.com/scheduling-jobs-with-python-crontab/
[onion-link]:http://www.4kwzfw7s2nh3viq3.onion/
[blog-link]:https://kushaldas.in/posts/setting-up-authorized-v3-onion-services.html
