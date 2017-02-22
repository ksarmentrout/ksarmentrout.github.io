+++
date = "2017-02-21T17:58:43-05:00"
title = "Techstars Week 2"
draft = false
categories = ["Techstars"]
description = "Mentor Madness Pt. 1: Introducing Automation"
tags = ["Techstars", "startups", "Python", "scheduling", "automation"]
type = "post"

+++

### Mentor Madness

is the name of weeks 2-4 of Techstars, during which a stampede of mentors descends upon the Techstars offices to 
offer individualized advice to companies in strictly limited 30 minute blocks. I'm one of the two Associates 
running the scheduling and logistics for Mentor Madness, and it is an intense undertaking. 

Quick numbers for week 1:
* 13 Companies
* 10 Associates (+1 Junior Associate)
* 5 Business days
* 6 Simultaneous meeting rooms
* **362 TOTAL MENTOR MEETINGS**

I now know the difference between being busy and being productive. Coordinating this scheduling kept me *busy*!

Each meeting contains one mentor, one company, and one Associate. When scheduling,
not only do the schedules of the companies need to be taken into account, but equally importantly, the companies,
mentors, and even Associates all have preferences for who they would like to meet with. Technical Associates benefit
from sitting in on mentors with technical backgrounds, for example. And each mentor is best suited to help the specific needs
of certain companies. The mentors, companies, and Associates all need to be notified of their meetings, especially
when changes inevitably happen. 

In preparation, I made a few tools to make my life substantially easier, and I can't imagine how hectic the 
system was in previous years:

1. Automatic notifications to companies and Associates if they were scheduled for new meetings or had one 
cancelled. 

The master schedule is simply a Google spreadsheet with a separate tab for each day, which allows it to be 
displayed on a TV all day for reference and intuitively edited by multiple people. There are probably better 
options, but it works for now. Some Python and the Google Sheets API, along with a lot of dictionaries holding 
company and Associate contact info, was able to monitor each of these days for changes and then send an automatic
email alert to the relevant parties about the change. The alert included whether or not the meeting was added or
cancelled, the time, the room, and the mentor who it was with. This I have running on crontab to check for changes
every 12 minutes. 

2. Generation of daily and weekly schedule summaries. 

The bot from above that looked at the Google Sheet and parsed out changes was also able to collect all meetings 
for each company and Associate. I used this to send individualized summaries of the following day to everyone, and 
do the same at the beginning of each week. The same feature helped me auto-generate emails to each of the mentors,
who I notified about their schedules a few days in advance. I later patched the notification bot to include the full updated
schedule for the day, after a few people requested the feature. 

3. Google Sheet population from youcanbook.me

The previous two bot features ran for the full first week. They had some messy moments (like when I originally
wrote them to check for 5 rooms and we started using a 6th that people subsequently didn't get updates about),
but overall helped cut down on a lot of manual emailing and schedule monitoring. I was doing enough as it was!

Over the weekend, though, I discovered how the mentor names had been appearing in the spreadsheet in the first
place, and it was from another Associate manually going through the email notifications sent from youcanbook.me
after a mentor used the site to make an appointment. It was so tedious! On Sunday (and I know I'm getting ahead
of myself chronologically, but it fits with the subject of this post), I put together a web app in Flask with 
dedicated endpoints listening for POST requests. Unfortunately, youcanbook.me doesn't support webhooks natively,
but it does integrate easily with Zapier, which can send its own! So three different webhooks are now up and running,
sending information whenever someone makes a new booking, changes, or cancels the booking through the site. My 
web app is hosted on Heroku, and upon receiving one of these POST requests, it automatically looks for a free room
on the Google Sheet and fills in the mentor's name! That should save a lot of manual data entry over the next two weeks.

4. Google Calendar integration

When I rolled out v1.0.0 of the bot, the first (and second, and third...) question I got was "can it send out Google
Calendar invites?" At the time, the answer was no, because I had sunk a good amount of time into it already and had
other projects I was working on. Over the weekend, though, I was on a roll with it and decided to tackle Calendar
integration as well. Turns out, it wasn't so bad! It actually took less time than debugging my webhook receiving 
endpoints did! I now have 24 dedicated Google Calendars shared with the appropriate parties that tell them only
when their own meetings are, and it updates whenever my notification bot runs!

### Overall 

My goal moving forward with these semi-connected parts is to fully document it and incorporate it all into the 
Flask app with a UI, so I can leave it as a gift for future Techstars classes. I'm sure the capable tech Associates
coming after me will be able to iterate on it, make it better, or even decide that a different workflow entirely 
is more appropriate! But I'm very happy with my ability to automate some of my own responsibilities with such 
effective end results. It has been heartening to hear about how much the companies rely on the notifications 
my bot shoots out in order to keep up to date, especially given how hands-off it is on my end at this point!

I guess this post turned into a technical overview, so next week I'll give my impressions on the mentor meetings 
themselves! 


