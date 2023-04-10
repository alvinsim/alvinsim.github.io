---
title: 'Automate It!'
date: Fri, 25 Mar 2016 10:53:59 +0000
draft: false
tags: ['automate', 'blog', 'buffer', 'hack', 'ifttt', 'pushbullet', 'scripts', 'windows']
---

![Automation](http://www.alvinsim.com/wp-content/uploads/2016/03/automation.jpg)  
Image Credit - [Eugen Stoll](https://www.flickr.com/photos/massenpunkt/) (_[Creative Commons License - CC BY-NC 2.0](https://creativecommons.org/licenses/by-nc/2.0/)_)

Machines are wonderful. They help us to be productive by doing the things we don't want to do or can't do, whilst we can focus on other important things.

Yes, I am **LAZY!** I write scripts or let services, like [IFTTT](https://www.ifttt.com) (_If-This-Then-That_), to do things for me.

This is how I automate some of my daily routines.

1\. Script to update source code from repository, build and deploy to local Apache Tomcat
-----------------------------------------------------------------------------------------

At work, one of my morning routines is

1.  Update working copy source code from the SVN repository.
2.  Change Windows timezone to "GMT Standard Time" (_Otherwise the build test would fail_).
3.  Build web application using `ant`.
4.  Deploy the packaged `war` file to local Apache Tomcat instance.
5.  Open browser to test if the build or deployment was successful.
6.  If successful, change timezone back to "Singapore Standard Time".

I put all these actions into a Windows BAT File and have the script running while I do other things, such as checking my email inbox and my tasks list.

1.  To update source code, I used the `TortoiseProc` command. Example: `TortoiseProc /command:update /path:"path\to\sourcecode" /closeonend:2`. For more information on how to use `TortoiseProc`, you can refer to the [TortoiseSVN Documentation Appendix D](https://tortoisesvn.net/docs/release/TortoiseSVN_en/tsvn-automation.html).
2.  To set Windows' timezone, I used the `tzutil` Windows command. Example: `tzutil /s "GMT Standard Time"`. This will set the timezone in Windows to "GMT Standard Time". For help to use this command, type `tzutil /?`.
3.  To test the `war` file deployment, I used the `call` command to run Apache Tomcat's `startup.bat`. Then I used the `pause` command to pause the script for 30 seconds to wait for Apache Tomcat to startup. AFter that, I use `curl` to query the URL and print out the `HTTP Status` code e.g. `HTTP 200 OK`. By looking at the `HTTP Status` code, I will know if the deployment succeeded or failed.

2\. Script to backup files
--------------------------

Windows has the command `robocopy`. Using this is more efficient than using the `copy` command because `robocopy` allows synchronization of directories. This means that `robocopy` will only copy modified files or directories, and remove files or directories if they were deleted from the source.

In my script, the command looks like this.

```
robocopy \source\path \destination\path /Z /MIR /R:10 /W:10 
```

To explain the command further

*   `/Z` - Restartable mode. If a file was partially copied due to interruption, the next run of `robocopy` will pick-up where it has last left.
*   `/MIR` - Mirror the directories and files between the source and destination paths. When source files or directories are removed, the same is removed at the destination path.
*   `/R:10` - Retry to copy the file if it was unsuccessful for a total of 10 times.
*   `/W:10` - Wait 10 seconds before retry copying the problem file.

For more information, you can use the command `robocopy /?`

3\. IFTTT - backup new photos/videos on phone to Flickr
-------------------------------------------------------

I have a Flickr account with 1TB storage space. This IFTTT recipe will "backup" photos and videos in my phone to my Flickr account. When new photos or videos exists in my phone, IFTTT will then send a copy of the photo/video to Flickr.

By doing this, I do not have to worry if my phone becomes a brick because my photos and videos are safe in Google Photos (_I enabled this feature in my phone_) and also Flickr.

4\. IFTTT - add Swarm/FourSquare check-ins to Google Calendar
-------------------------------------------------------------

I use this IFTTT recipe to create a log of interesting places I have been to (_checked-in via [FourSquare](https://foursquare.com/)_) to my Google Calendar. It also will save the GPS location of the place.

Few weeks ago, my wife asked "What's the name of the place we went to for AW's (_youngest daughter_) birthday last year?". I couldn't remember the name, too. But I was able to find the name by searching the checked-in in my Google Calendar.

5\. IFTTT - notification to phone at 7:00 AM with the day's weather forecast
----------------------------------------------------------------------------

It is good to know what the weather will be like throughout the day. And this is how I do it with this IFTTT recipe.

6\. IFTTT - notification to phone when people mentions me \[@alvinsim\] in Twitter
----------------------------------------------------------------------------------

I'll receive a notification on my phone when people mentions me in Twitter. This is useful for me because now I don't login to Twitter that often. But I still do post things to Twitter, but via Buffer.

7\. Buffer - schedule social media postings
-------------------------------------------

[Buffer](https://buffer.com/) is a very handy app. It allows me to post to other social media accounts. I have Twitter, Facebook and Linkedin linked to my Buffer account.

Besides posting to the different social media accounts, I also use Buffer to schedule the postings. This is what I do when I post a blog post to my website. I would publish the blog post first. Then use Buffer to schedule the announcement at 10 AM (MST) the next day to my Twitter, Facebook and Linkedin followers.

If you need additional features e.g. connect to RSS Feeds, analytics of your postings, connect with more social profiles, yada yada yada, you can upgrade to their Awesome Plan. Check their website for pricing. For me, the free plan is suffice.

8\. Pushbullet
--------------

_This may not be a automation hack, but I want to share this as a hack I use daily._

I have [Pushbullet](https://www.pushbullet.com/) installed in both my Windows laptop and my phone. The thing I Find useful about this app is when I am doing work on my laptop and my phone is far away from me, e.g. in another room, an alert will appear in Windows notifying me when I have a call, a new SMS, new WhatsApp messages, etc.

Another use case I Have is when I am doing online banking and I need to request for a one-time pin (via SMS), I do not have to pickup my phone to see the pin number. Because the it is visible in the alert window.

* * *

If you have any automating or time-saving hacks, do share in the comments below.