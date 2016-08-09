+++

tags = ["hugo", "git", "github", "html", "css", "website"]
categories = ["Misc"]
date = "2016-02-22T10:36:26-05:00"
description = ""
draft = false
type = "post"
title = "Building this Site"

+++

I've been wanting to build a website for a while. Mostly just so I know what the process is like, but also to have a place
to post my work and I thought that maybe going through all the effort of setting up a blog will motivate me to actually
use it. The first place I started learning, some time ago, was with Codecademy and working through their HTML/CSS modules. 
Those were pretty interesting as a beginner and introduced some of the concepts, but despite the praise and awards it gave
for following instructions, there was so much hand-holding that I had very little retention. I certainly didn't feel confident 
starting from scratch.

Jumping to this year, I went to a HTML/CSS bootcamp-like seminar a few weeks ago that was very well taught. It introduced me
to using Visual Studio as a coding environment, and went over the basics of HTML/CSS. I was inspired from this to go on
and construct my first site using the skills from that class and the [Bootstrap framework](http://getbootstrap.com/). 
The end result from generally following a template online was this:

<img src="/img/building_site/old_site.jpg" width=100%>
<br />
<br />

...which was ok. Simple, extremely easy to navigate (being only barely taller than the browser window), but with limited
functionality. I could have added more sections to include things like the "about" and "projects" descriptions that are
on my new landing page, and I even began a redesign process to include those and change the color scheme/layout. I had 
big plans. Though I did ultimately want a blog option, and I had no idea how to implement or host an easily extensible 
site with an unforeseen number of posts. 

I then went looking for options and came across Hugo. Well, actually came across Hugo and Jekyll, but settled on Hugo so I
wouldn't have to deal with the Ruby dependencies involved in Jekyll, and because Hugo seemed more straightforward to set up.
There was, however, a bit of a learning curve. I found two templates I liked, one for a landing page and one for a blog, 
and wanted to combine them so that one linked to the other. This is where I was very thankful for the HTML and CSS I'd 
learned, because I was able to identify what features of each template I wanted to implement, and how to cherry pick from
them to create a unified site. It took some time to learn how to use the syntax of Hugo and Go to wrangle everything together
(e.g. with the `{{ }}` notation and the relationship between content pages and layout files), but I soon became comfortable
enough to get everything running locally using `hugo server`. 

The final obstacle was hosting. I'd used Git while making my previous site and had learned how to push everything to GitHub
for hosting via GitHub Pages, but organizing the two separate repositories for the `/public/` folder and the source files
(and why they were even needed in the first place) took a long time to figure out. After reading and re-reading several 
different guides on hosting Hugo pages with GitHub, I was eventually able to set up a streamlined way of pushing my content
up and successfully hosting it. Going to my website address and not seeing a big 404 was a huge sigh of relief. 

Overall, tackling Hugo alongside new ways of using HTML, CSS, and Git was challenging, but I loved figuring it out. Working
on the site became addicting for a few days, and I found myself spending probably more time than I could afford on creating
and curating how I wanted it to look. Now that it's live and the workflow of updating it is set up, I'm really enjoying 
the simplicity of creating new posts and how well Hugo and my short .sh script handle building everything. It's certainly
not done (as of this writing, a few of the clickable blog features go nowhere), but I'm very happy with how it is turning out
and excited to document my next projects. 



