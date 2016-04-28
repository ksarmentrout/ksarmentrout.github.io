+++

date = "2016-04-06T14:33:07-04:00"
title = "EEG Overview and Control Plan"

tags = ["EEG", "BCI", "human-robot interaction", "projects", "java"]
categories = ["Projects", "EEG"]
description = "In which I think about moving"
draft = false
type = "post"

+++

Despite the huge jump time leap between posts (almost 2 months?) about this EEG system, I've been working on it this 
whole time. So I'm going to try to make a few smaller posts as sort of a retrospective look at what that process was like.
 This first mini-update gives an overview of EEG and deals with how I first approached getting data from the headset.
 
 When I left the last update, I had just gotten the Emotiv EPOC headset to work and I was able to see the raw data from
 the electrodes. Great! The problem was where to start turning those squiggly traces into usable signals.
 
 <br/>
 <img src='/img/emotiv_epoc_testbench.png' width=100% float="middle">
 <br/>
 <br/>
 
 Above shows the squiggly traces in question. This is TestBench, software made by Emotiv, that shows the real-time output 
 from each of the 16 electrodes. On the left is the electrodes' placement on the head. Each of these electrodes is picking
 up the weak changes in electric potential that are caused by neurons firing in the brain. So yes, an EEG system is reading 
 your mind. But before you get too excited, I have to note that it's still pretty bad at it, for these reasons:
 
 * The electric signal from a single neuron firing is very tiny, so only the overall fluctuations of 
 large neural populations can be detected. This means that you can't pinpoint exact brain regions to measure from.
 * All of the parts of your head that so helpfully keep your brain from falling out unfortunately lie between the signal
 source and the detector. So the already tiny electrical signals need to make it through several layers of
 tissue and fluid, your skull, and often hair before they get to the EEG headset. This adds a lot of noise and also makes
 it impossible to get information from inner brain regions.
 * The system is VERY sensitive to movement and EMG (muscle) signals. Your face contains an incredibly intricate and well-
 controlled arrangement of muscles, which sit on top of the skull and create their own electrical signals. If you so much
 as clench your jaw, wiggle your ears, or even blink while wearing the EEG, those signals overwhelm any cortical signals.
 The same goes with moving your entire head at all (in EEG research, the subject's head is often held in place to prevent
 this).
 * None of the information this system picks up can be used for any of the sci-fi mind-reading devices you can think of.
 It is impossible to use this to detect mental commands like "turn right" or "drive home," it just gets overall changes
 in neuronal activity.
 
 So why use it? It provides in broad strokes a sense of the overall brain activity and can provide an assessment of
 states of wakefulness or alertness, used for research into [sleep disorders](http://www.hopkinsmedicine.org/healthlibrary/test_procedures/pulmonary/sleep_study_92,p09032/)
 , [attention](http://www.sciencedirect.com/science/article/pii/S1388245702000366), and even [meditation](http://www.sciencedirect.com/science/article/pii/S0304394001020948). 
 It provides real-time signals, so even though they might be lacking specifics, you're at least kept up to date. 
 By performing a [Fourier Transform](https://en.wikipedia.org/wiki/Fourier_transform) on the time-varying signals, they
 can be viewed in terms of frequency bands, i.e. oscillations in overall brain activity occurring at different speeds.
 These have been divided up into [a few labeled ranges](https://en.wikipedia.org/wiki/Electroencephalography#Wave_patterns)
 that are referred to when monitoring changes in brain activity.  
 
 Some of these changes correspond to mental commands to move. The areas controlling movement in the brain are right on top,
 in the outermost layer of the brain. They're also in pretty much the same spot for everyone, making them good candidates for
 targeting with EEG. One way to use this is through "motor imagery," where instead of actually moving part of your body, 
 you instead just think really hard about it. There have been [a number of projects](https://sites.google.com/site/fabienlotte/pictures-and-videos)
 employing this as a control scheme (outside of this one lab as well, but I think some of those applications are interesting).
 Of course, you could also just physically move part of your body and that would create a larger signal from the motor cortex,
 but it looks a lot less futuristic to be flailing an arm about while using one of these. 
 
 Overall, by describing each of these parts, I've basically outlined my plan for a control scheme. I am discriminating
 between two mental states: motor imagery of right hand/arm vs. left hand/arm movement. I accessed the raw data from
 the EEG using a Java program and the Emotiv SDK and recorded trials during which I imagined moving each of my arms
 sequentially. I've sliced them up into 1-second intervals and done an FFT (Fast Fourier Transform) on each of those
 intervals. The goal is that when I imagine left hand movement, there will be a detectible change in right brain activity
 within one of the frequency bands mentioned earlier (in this case alpha and beta, going from ~8-14 and ~15-30 Hz, respectively), 
 and vice versa. This difference will be used to predict in further trials whether I am moving my right or left hand in any
 given second. If I assign these two states to be 0 and 1, that prediction can be used as a control signal for some other
 device or program while I remain motionless. So basically, it'll read my mind.
 
 