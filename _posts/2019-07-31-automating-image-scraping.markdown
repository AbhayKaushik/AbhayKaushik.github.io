---
layout: post
title:  "Automating Image Scraping"
date:   2019-07-31 10:09:50 +0530
categories: jekyll update
---
Yeah, this is the second part of image scraping blog. You see, even after making the script, I was not satisfied.

First, I will have to execute the script every time I want to see the latest images (obviously..) but I may forget to run the script one morning (it’s really difficult to be regular)

Second, the sub-reddits that I have selected are very active and new posts keep popping up. 
So, it’s quite possible that I may loose some of them if I don’t check on them regularly.
Reddit only loads the top posts according to preference and you have to scroll down to load more, which makes it difficult to scrape the entire page and you only get these top posts.

Now, as you may have guessed, the answer to this : automation! So, I searched on how to automate scripts, and I stumbled across cron jobs.

Basically, cron is a time-based job scheduler in Unix-like computer operating systems. 
Cron is used to schedule jobs to run periodically at fixed times, dates, or intervals, especially by those maintaining software environments.

You can learn more from this [link][cron-link]

First I had thought of automating this process in a cloud vm, and host a site with periodically change the html, but it is diffcult to do without a billing account (I am not going to use credit cards just yet :) )
I stumbled across many searches and methods and finally reached mongodb along with heroku.But it'll take more time, so I will cover it in some other post.

Now, I will the run the script that I made earlier with some changes. Actually, I learnt later that you can access the rss feeds of a site by using .rss 
I tried wth .xml, but it doesn’t work everytime.
 
Turns out, their xml and rss equivalents don’t have img tags, instead they have a description tag with the image details. 
This won’t work with my script (The turnoff link is an exception as it has the img tag. I think these files are dependent upon the maintainers of these sites)

```python
#Code here
```

## Chronic Cron

Chronic: continuing or occurring again and again for a long time 
Cron: process or task that runs periodically on a Unix system
Chronic Cron: process or task continuing or occurring again and again for a long time periodically on a Unix system

Now, I had already seen crontab before learning about cloud schedulers, so I was wondering of I could write a cron job within my computer to excute the script.
 
Before I could try this, I stumbled across schedule (cron for humans) [library][schdule-link] and then decide to use that for my script. 

So, again I modified my script (in development, you will always have to makes changes to imrprove, so you must not be afraid to do that. Though to tell the truth, I am pretty much frustated by myself considerng the number of changes I am making :| )

Now, I decided to add the cron job in my local computer. The only downside will be that the process will be skipped if my computer is not on or I am not using it. 
This is particularly not the case in my vacations but could be possible when my college starts.

So, first I tried a simple cron job of inserting text in an empty file :

```shell
20 17 * * * echo "This works" > /home/abhayk/Documents/Coding-Blocks-ML/img.txt 
```
I checked the syslog in /var/log/syslog and saw this among the lines:

CRON[1321]: (abhayk) CMD (echo "This works" > /home/abhayk/Documents/Coding-Blocks-ML/img.txt )

Now, I had to run a python script in my cron job.

First, make sure that your python script is executable.

```
chmod +x imagegrab.py
```

After some more searching, I found that there some cron job handling in the form of locks maybe (yet to read), but it is somewhat difficult.

And then I found just the thing, schedule library [link][schedule-link]

The main advantange is that in case my computer is not on(working state), then it'll will wait until that is not the case and then initate the downloads.

After all this, the only problem left is to make sure that my laptop stays connected to the net.
Not entirely independent till now.But hey! It's an improvement.Atleast my script will run once a day in the morning (mostly without fail :P)

So, I added my entire code to a single function and then my script (hopefully the final one), was something like this:

== Insert Code ==

And here we are at the end of this blog. (Or are we? XD)

## Not Content Without Bonus Content

Now,I recently learnt to create a site in tor. 
So, here’s the [link] for the same. 
It may not work always as it is self-hosted (currently), but hey! it can be whatever I want. 

If you too want to make your own onion (especially if you have a server lying around), you can see this [blog][blog-link] by Kushal Das

[cron-link] : https://a.com
[schedule-link] :
[onion-link]:
[blog-link]:
