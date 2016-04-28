+++
date = "2016-04-27T21:47:18-04:00"
title = "EEG Initial Results"

tags = ["EEG", "BCI", "human-robot interaction", "projects", "java", "arduino"]
categories = ["Projects", "EEG"]
description = "Motor imagery results, hardware check, and new plan"
draft = false
type = "post"

+++

Where I left the last post was with my plan to use motor imagery (imagining left- or right-arm movement) to drive a motor
via the Emotiv EPOC EEG headset. In one-second intervals, the EEG would record brain activity, analyze the data, and return
a classification about whether the system predicted that the brain signals corresponded to left or right arm motion. The
classification was done by a support vector machine [(SVM)](https://en.wikipedia.org/wiki/Support_vector_machine) which had
been trained using 1000 seconds of labeled input data. Basically this means that I performed trials of motor imagery for
left or right arm motion and fed this information into this machine learning algorithm, which tried to separate the data
into these two groups. When a new data point (which in this case is one second of readings from the EEG headset) is given
to this algorithm, it determines which group the point belongs to and returns this guess as its classification. 

I tried this with motor imagery and the results were... poor. The highest classification accuracy shown from the test data
was only 53%, which is barely above chance (because there are only two possible options, chance performance is 50%, like
a coin toss). So as a sanity check, I decided to test the quality of the hardware I was working with.

I decided to determine if the system could pick up on whether I had my eyes open or closed, which is actually 
a lot easier than you might expect. An interesting thing about your brain is that in some frequency ranges (specifically
between ~8-15 Hz), the activity level changes _dramatically_ depending on whether your eyes are open or not. And this
change occurrs nearly very rapidly after opening or closing them. The paper I was comparing to (Barry et al. 2007) reported
that the activity level in this frequency range dropped by approximately 50% when subjects opened their eyes, so I expected
to see something when I replicated their study with the Emotiv EPOC. ...I didn't. The change I saw was negligable, amounting
to a drop of just over 1%. So that was a bust. 

Basically, the headset seemed to be very bad at detecting much of anything, at least from my observations. From this I
thought that motor imagery might not be enough, and maybe physical arm movements would be easier to detect. So the next
step was to re-do all of those test trials while actually moving each arm, which felt kind of silly. More on that in 
the upcoming last post about this EEG project. 

