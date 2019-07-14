---
layout: post
title:  "Scraping Images for Good"
date:   2019-07-14 10:08:57 +0530
categories: jekyll update
---

So, in #dgplug training, someone shared a blog on [depressed-developers][dd-link]. After that, we were suggested to try writing a script to retrieve the latest images that were published on the site.

I realised after searching for a while that what I wish to do is actually web scraping (web scraping was on my lists of things to learn, as I thought it would be very difficult)

I read some more links, got to know about [Beautiful Soup][soup-link] library and then wrote my script using it.The script is something like this:

```python
import requests
import urllib.request
import time
import os
from bs4 import BeautifulSoup

url = 'https://turnoff.us/feed.xml'
response = requests.get(url)

soup = BeautifulSoup(response.text, 'html.parser')
tag = soup.findAll('img')[0]

link = tag['src']
name = tag['alt']
name = '-'.join(name.split()).lower()

os.mkdir('./turnoff_Images/')
value = urllib.request.urlretrieve(link, filename = './turnoff_Images/'+ name + '.png')
print("Latest Image :" + name + " saved in turnoff_Images folder")
```

I did take help from this [link][data-scraping-link] though.

I was glad of this achievement.I learnt by myself, a thing which I thought was too tough to understand alone.
Now, this took me around 2 hrs until I posted the link to code on the channel. (yeah I know that’s too much time; I spent 30 mins procrastinating on how to send a proper message on the IRC)

Later, I started thinking on how I could make this into a project or hack to make my life easier.
And then the light bulb moment! I realised that I am lot into memes and art. Instead of scrolling through social media, (which seriously makes time disappear :| ) I decided to look where these memes are made. Turns out, some of the popular ones have a blog of their own.

Also, I wanted to check the sub-reddits on comic and unix-setups (ahem ahem, I think you got it XD).

So now I got a list of urls that have regular content on their sites. As I don’t need the related text,the RSS reader felt a bit overkill to me.
I decided to modify my python script and run it to get the new images from all these blogs.

### **Scaling Things Up**
 
Now, each of the blog was different so I studied the source HTML of each blog to see how the image I need can be extracted.

Sometimes, required images were not the within the first image tag of the page, as there were other images such as the logo and advertisements.
The good thing was that the source of these ads and logo had common substrings, which could be used to differentiate to get the required images.

```python
link = tag['src']
if 'external' in link or 'static' in link:
    continue
```

Also, sometimes the server was busy and I used to get a response [429][bad-gateway].To tackle that, I pinged the server multiple times with some pause(multiple requests without a break can get you flagged by the server, preventing you from getting any more requests through)

```python
response = requests.get('https://www.reddit.com/r/comics/')
tries = 0

#Make multiple requests to busy server 
while not response.ok and tries < 20:
    time.sleep(1)
    response = requests.get('https://www.reddit.com/r/comics/')
    tries += 1
```
Now, the only thing left was to make sure that I don’t get duplicate images.For that, I maintained a check.txt which stored the last links that were processed upon in the previous run.

```python
#Saving the last links to a file
#We will overwrite the file and enter new contents
with open("./check.txt",'w') as file: 
    for l in last_link:
        file.write(l)
```

The contents of the file were then loaded and each string when processed, was checked if it was present in the last links. As the most recent images are on the top, so after getting an old image link match, the processing was stopped. This is because all the images below would already have been processed in the previous run.

```python
n_link = link.split('?')[0].replace('preview','i')
if not n_link in check_list:
    response_list.append(n_link)
else:
    break
```

The response_list that was complete with all the relevant links, was then used to load the images and then store them in the images folder.

```python
os.mkdir('./Blog-Images/')
for link in response_list:
    img_name = link.split('/')
    for n in img_name :
        if 'jpg' in n or 'png' in n:
            name = n
    value = urllib.request.urlretrieve(link, filename = './Blog-Images/'+ name)
```

So, finally the entire script looked like this.

```python
#Initial Things to Load each Time
last_link = []

#Last Link list loaded
check_list = []
with open('./check.txt', 'r') as csvFile:
    reader = csv.reader(csvFile)
    for row in reader:
        link = ''.join(row)
        check_list.append(link)
csvFile.close()

#list to store the responses
response_list = []

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
        response_list.append(n_link)
    else:
        break
        
print(response_list)
last_link.append(response_list[::-1][0])

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
    if(response.ok):
        soup = BeautifulSoup(response.text, 'html.parser').findAll('img')
        tag = soup[idx]
        link = tag['src']
        idx += 1
        if not link.startswith('h'):
            #Adding https in the start to create a valid link
            link = 'https:' + str(link)
        last_link.append(link)
        if not link in check_list:
            response_list.append(link)
            

#--Saving the last links to a file --

#We will overwrite the file and enter new contents
with open("./check.txt",'w') as file:
    for l in last_link:
        file.write(l)

##Load the new images to the folder
os.mkdir('./Blog-Images/')
for link in response_list:
    img_name = link.split('/')
    for n in img_name :
        if 'jpg' in n or 'png' in n:
            name = n
    value = urllib.request.urlretrieve(link, filename = './Blog-Images/'+ name)
```
Off to see the new images my script grabs.See you next week!

[dd-link]: https://turnoff.us
[data-scraping-link]: https://towardsdatascience.com/how-to-web-scrape-with-python-in-4-minutes-bc49186a8460
[bad-gateway]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/429
[soup-link]: https://www.crummy.com/software/BeautifulSoup/bs4/doc/
