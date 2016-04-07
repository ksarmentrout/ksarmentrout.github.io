+++
categories = ["Projects", "EEG"]
date = "2016-02-18T20:21:56-05:00"
description = ""
draft = false
tags = ["EEG", "BCI", "human-robot interaction", "projects"]
title = "Starting the EEG"
type = "post"

+++

This post is a few days late, but I needed to get my website up and running before I could make it. The other day, I 
was finally able to start up the Emotiv EPOC EEG device I will be using for this project and observe my real-time neural
data. As expected, it was terribly noisy. Though I did learn a few things about the Emotiv software (with little thanks
to their documentation) and what causes disruptions in the EEG signals. Namely, blinking is extremely easy to detect
and clenching my jaw makes the traces go crazy, so I can't be doing either of those during the actual experiments.

First impressions: this setup is very cool, though I can immediately see why it is of limited use as a control scheme. 
Here I go anyway. The first steps from here are to go through the example code provided by Emotiv on how to detect and 
record the signal values outside of their GUI, a process that will most likely be done using Java and Eclipse. Currently 
unsure about how I will do the analysis. A roadblock I'm already seeing is that the Emotiv software makes it difficult
to set cue/marker points and it also starts recording immediately upon running the software. Considering I'll be running
tests on myself, I'll either need to write a cueing program from scratch to get training data or use their manually-
triggered system, and try not to think too hard about starting and stopping it, I suppose... We'll see how that goes.

Overall goal for this project: be able to generate and discriminate between two discrete signals (other than neutral 
baseline). While the end effector is still undetermined, these two signals could be used for something like a left/right
scheme, or for on/off.

Big thanks to Jake at [NeuroPlus](http://www.neuropl.us/) for generously allowing me to use one of their EEG headsets!