+++
date = "2016-05-12T20:39:01-04:00"
title = "Final EEG Update"

tags = ["EEG", "BCI", "human-robot interaction", "projects", "java", "arduino"]
categories = ["Projects", "EEG"]
description = "Not much better than a coin flip"
draft = false
type = "post"

+++

The previous post about my initial EEG results talked about how I initially started by using motor imagery, i.e. thinking
about moving my hands instead of actually moving them, to control a device. That didn't work. The support vector
machine (SVM) that was performing the classification between left- and right-hand movement was performing only slightly
better than chance, about 53% accuracy or so. To try and improve that number, I decided to use actual arm movements. I
that this would not only increase the amount of active motor cortex, but also standardize the brain activity across
samples. I set a metronome to 60 beats per minute to make sure I was doing a complete arm movement each second. 
When I was only visualizing arm motion, my imagined movements would not be consistent over time and my mind could wander,
so the metronome ensured that my arm would be in the same position at the same point of each 1-second sample. 

With this new paradigm, I recorded another 100 trials for each arm and trained the SVM on the first 80. The machine did...
better. Only about 3% better, giving my maximum accuracy (when categorizing the 200 seconds of training data) up to 56%.
Based on this result, I'm not sure if the change in performance means that there was really higher accuracy due to the
actual arm movements, or if the system was still performing at approximately chance but with a high variance. Either way,
the benefit from the real arm movements is not anywhere near large enough to justify using such a control scheme instead
of a conventional joystick. If the subject is moving their real arm anyway, why not just use a much more intuitive,
tactile system? 

Based on my experiments, I've found that the Emotiv EPOC system is not sufficient for reliable, accurate
control of an external device via motor imagery or by detecting actual motor commands. Of course, there are probably
other machine learning algorithms I could have tried that would have improved the system performance. Some examples
I came across in several papers are common spatial pattern analysis and linear discriminant analysis. However, time
constraints left me unable to implement them, so their effectiveness remains unknown. Judging by the extreme similarity
between average FFT spectra across left- and right-hand movement conditions and the huge overlapping variance in each 
case, however, I don't know how much improvement is possible for classification.

Overall, I found the system lacking and unable to accurately detect changes in brain activity, even across some broad
frequency bands like those used in its built-in software. Due to its requirement of wet electrodes, high sensitivity
to movement and EMG artifacts, and low signal detection accuracy, this commercial system does not seem viable as a 
control device. 

