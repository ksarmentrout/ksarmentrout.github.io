+++
date = "2016-08-08T19:20:11-04:00"
draft = false
title = "IoT Candy Dispenser"

tags = ["projects", "to-do", "DIY", "API", "Photon"]
categories = ["Projects"]
description = "My first real tinkering project"
type = "post"

+++
<div class="col-lg-7" style="padding-left: 0px;">
<p>
I love to-do apps. Specifically Wunderlist, and I don't think it's an exaggeration to say that I rely on
it at this point, now that I've been using it for several years. I make lists for everything, including an
item that is reminding me to make this very post. One of the best things about Wunderlist in particular is
that I've come to enjoy the bell sound effect that accompanies checking off an item. It's just so crisp and
satisfying that it makes the sense of accomplishment that much sweeter. Earlier this summer, I was apparently
channeling my inner Pavlov and thought that in addition to just the bell, if my to-do list could reward me
with something tangible, it might be an even better incentive! So I began designing my first ever real 
tinkering project: a smart candy dispenser.
</br>
</br>
</p>
</div>

<div class="col-lg-5" style="padding-right: 0px; float:right;">
<figure>
<img src='/img/candy_dispenser/final_pic.JPG' width=100%>
<figcaption style="text-align:center; font-size:11pt;">Finished product first! Low M&Ms from all the testing.</figcaption>
</figure>
</div>


## Software
I had been thinking about connected devices in part due to a short workshop on the Particle Photon that I
had taken here at Duke. They have some amazing resources for makers, primarily thanks to the [Innovation Co-Lab](https://colab.duke.edu/),
which was the host of the workshop. The workshop not only gave us a primer on how to use the Photon (which was
pretty straightforward after my experience working with an Arduino), but they sent us each home with one! So from
day one I knew the Photon would be the brains of the device. 

Writing the code was fairly trivial. I only needed to drive one servo for my mechanism, so the only part I needed
to figure out was how to connect it to the apps. Even though I only use Wunderlist, I ended up connecting the 
dispenser to both Wunderlist and Todoist, so it now responds to my activity within either app. The reason for this
is because the webhook functionality of the Wunderlist API is terribly imprecise. You can set a webhook for a 
particular list you've made, but then the webhook is activated whenever that list is updated *at all*. This 
includes adding and deleting items, as well as completing them. This of course isn't ideal because I don't
want to be rewarded for giving myself *more* to do (or giving up on items?). However, my only other option
would require polling the Wunderlist server intermittently to check, for each of my lists, the API call
for completed items, and compare those lists to stored versions to see if anything had been changed. This would
not only be far more complicated, but would also require that I leave the Photon on 24 / 7 and would potentially
separate item completion and reward by a significant amount of time, depending on how often I queried the server.
Ultimately, I went with the webhook, and I'll use it sparingly. The Todoist API was far better and I was able
to create webhooks that respond only to checking off items. 
</br>
</br>

## Hardware
This was the tricky part. I'd never really designed anything before, and I wasn't entirely sure how the
mechanism was going to work. So it ended up going through many iterations, in part due to my own learning
process, and in part due to failing 3D-prints. My printing was done in the incredible wall of 3D-printers at
the Innovation Co-Lab, and even in the summer they're overworked. I used TinkerCAD for my modeling. It's not
very powerful, but it's very easy to use and accessible without spending anything on professional software.

<div class"row col-lg-12" style="display:table">

<div class="col-lg-5" style="padding-right: 0px; float:right; display:table-cell;">
<figure>
<img src='/img/candy_dispenser/bad_print.JPG' width=100% style="padding-top:6px;">
<figcaption style="text-align:center; font-size:11pt;">Poor thing never stood a chance.</figcaption>
</figure>
</div>

<div class="col-lg-7" style="padding-left: 0px; display:table-cell;">
<p>
After considering a few designs, my first plan was to have the servo control a flap that ran parallel to 
the front wall of the dispenser, and would swing to the side to allow M&Ms through. The M&Ms would be coming
down a chute leading from the top of the box and be up against the flap until it swung open. My design included
the base of this chute as a part of the shell of the dispenser so it would all print in one go. After two failed
prints of this, I decided to break it into smaller components so that I would have a better chance of printing
each of them without the nozzle clogging or the printer running out of filament (hard to monitor when printing
remotely). 
</p>
</div>
</div>

<div class"row col-lg-12" style="display:table; padding-bottom:15px;">
<div class="col-lg-5" style="padding-left: 0px; padding-top: 10px; float:left;">
<figure>
<img src='/img/candy_dispenser/first_design.JPG' width=100%>
<figcaption style="text-align:center; font-size:11pt;">First design with vertical flap. Shell and lid in the background.</figcaption>
</figure>
</div>

<div class="col-lg-7" style="padding-right: 0px;">
<p>
The picture on the left shows the first full build of my initial idea. The part I'm holding is actually two pieces
that fit together with a ramp in the M-looking part leading to a chute down the back. Similarly, the shell in 
the background is two pieces: the base and three vertical walls and the lid that fits on top. Once I put this together
along with the rotary I printed for the front and tested it with real M&Ms, there were several problems. The M&Ms
would bottleneck in the chute, the rotary was poorly designed, and even when the M&Ms could get through, they didn't
have enough force to make it over the gap that the rotary left before the tray. So back to the drawing board.
</p>
</div>
</div>

After toying with some other ideas for a day or two and trying to design something that would work and still make
use of the parts I'd already printed, I arrived at the brilliant idea to... just turn the thing around by 90 degrees.
I know. Exciting stuff. But this way the servo was at the top, meaning the flap would be right at the base of the
jar of M&Ms and also only a few M&Ms at a time would be traveling through the chute so they wouldn't get stuck.
I redesigned the lid to make it contiguous with the upper piece in the above photo so it would hover above the
rotary piece that would be moved by the servo. After re-printing the L-shaped chute piece to account for its new
use, I assembled it into the nearly complete configuration below.

<!---
<div class="col-lg-12">
<figure>
<img src='/img/candy_dispenser/test_build.JPG' width=60% style="display:block; margin-left:auto; margin-right:auto;">
<figcaption style="text-align:center; font-size:11pt;">First design with vertical flap. Shell and lid in the background.</figcaption>
</figure>
</div>
-->

<div class"row col-lg-12" style="display:table; padding-bottom:15px;">
<div class="col-lg-6" style="padding-left: 0px; padding-top: 10px; float:left; display:table-cell;">
<figure>
<img src='/img/candy_dispenser/test_build.JPG' width=100%>
<figcaption style="text-align:center; font-size:11pt;">Test build with Photon and batteries.</figcaption>
</figure>
</div>

<div class="col-lg-6" style="padding-right: 0px; padding-top: 10px; float:right; display:table-cell;">
<figure>
<img src='/img/candy_dispenser/with_lid.JPG' width=100%>
<figcaption style="text-align:center; font-size:11pt;">Adding the lid and rotary piece.</figcaption>
</figure>
</div>
</div>

On the left is my test to make sure that everything fits and that the Photon is responding and able to drive
the servo. Confident that it worked, I added the rotary piece and lid. This was in the workshop where I also 
sanded down the bottom of the lid to fit the rotary piece and mounted the on/off switch onto the front.

Once those were put together, I could screw the back panel on to enclose it, and add the jar of M&Ms to the top!
I was done!! Describing this undertaking in hindsight makes it sound more simple than it was to design, mostly
because I'd never done something like this from scratch before. I learned a lot about the iterative design
process during this, including an increased mindfulness of silly mistakes. Even though the design isn't optimal
and could have better aesthetics, it works as I want it to and I'm proud to have taken something from concept 
to reality. I think I'll wrap this up here now and post it; I've earned some M&Ms.

</br>
## Misc Photos
Here are a few more pics I took to flesh out the story of development. Also included are some 3D print progress
gifs. Each printer in the Co-Lab has a webcam attached to monitor prints and each automatically produces a time-lapse
video of the print. The two below are my favorites

<div class="col-lg-12" style="padding-bottom:15px;">
<div class="col-lg-offset-3 col-lg-6" style="padding-top: 10px; display:table-cell;">
<figure>
<img src='/img/candy_dispenser/initial_testing.JPG' width=100%>
<figcaption style="text-align:center; font-size:11pt;">First testing of the horizontal flap.</figcaption>
</figure>
</div>
</div>

<div class="col-lg-12" style="padding-bottom:15px;">
<div class="col-lg-offset-2 col-lg-8" style="padding-top: 10px; display:table-cell;">
<figure>
<img src='/img/candy_dispenser/new_top_lid.gif' width=100%>
<figcaption style="text-align:center; font-size:11pt;">Printing the final lid.</figcaption>
</figure>
</div>
</div>

<div class="col-lg-12" style="padding-bottom:15px;">
<div class="col-lg-offset-2 col-lg-8" style="padding-top: 10px; display:table-cell;">
<figure>
<img src='/img/candy_dispenser/shell.gif' width=100%>
<figcaption style="text-align:center; font-size:11pt;">Printing the dispenser shell.</figcaption>
</figure>
</div>
</div>

<div class="col-lg-12" style="padding-bottom:15px;">
<div class="col-lg-offset-1 col-lg-10" style="padding-top: 10px; display:table-cell;">
<figure>
<img src='/img/candy_dispenser/print_graveyard_2.jpeg' width=100%>
<figcaption style="text-align:center; font-size:11pt;">Graveyard of failed or unused prints. The two at the top
are the original failed shells with the chutes included. The one on the top right wasn't completely done but told 
me enough to know that I needed to re-do the measurements and design of the center piece. The two on the left are
unused versions of the center piece that ended up not having quite the right measurements after I decided to turn
the chute by 90 degrees. The bottom two are variants of the rotary piece: the left one is v.1 of the newer horizontal
flap design (with a servo arm pre-emptively super-glued in...) and the right is a vertical rotary with incorrect sizing.
There is nothing wrong with the remaining two pieces, but they belonged to the old design and could not be used.</figcaption>
</figure>
</div>
</div>

<div class="col-lg-12" style="padding-bottom:15px;">
<div class="col-lg-offset-3 col-lg-6" style="padding-top: 10px; display:table-cell;">
<video width="320" height="568" controls>
<source src="/img/candy_dispenser/demo_vid.mp4" type="video/mp4"></source>
Your browser does not support the video tag.
</video>
</div>
</div>

<div class="col-lg-offset-3 col-lg-6">
<p style="text-align:center; font-size:11pt;">
Video showing the dispenser working in response to checking off a Todoist item. </p>
<p style="text-align:center; font-size:11pt;">
I know, I know... it's a vertical video... It was for Snapchat, I'll post a proper one eventually.
</p>
</div>
