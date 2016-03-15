+++

date = "2016-03-07T22:00:41-05:00"
tags = ["twitter", "bot", "neural network", "automation", "asoiaf", "game of thrones", "harry potter"]
categories = ["Projects”, “Misc”]
description = ""
draft = false
type = "post"
title = "Twitter Bots"

+++

This past weekend I decided to build a Twitter bot. I'd never done this before, but considering I'm relearning Python
for lab projects and I have my first ever Twitter account as of a few weeks ago (several years late, I know), I thought
I'd give it a go. To jump right to the results, the two bots can be found [here](https://twitter.com/asoiaf_bot) and
[here](https://twitter.com/hp_nonquotes).

First question: what should the bot do? I had spent all day researching machine learning for a separate project, so I thought to try
and find a speech-generating neural network (NN). I came across [the one described here](http://karpathy.github.io/2015/05/21/rnn-effectiveness/)
and was fascinated by the clear and concise the way the author described it, and the surprisingly coherent results.
Surprising because this particular neural network is character-level, meaning once it learns from a set of training data,
it samples the data and generates output one character at a time. This is in contrast to a lot of other text generating
programs (like autocomplete on a smartphone) that often use Markov chains to write output one full word at a time, based on
the occurrence and order of the words in the training data. This program is appropriately called [char-nn](https://github.com/karpathy/char-rnn),
written by [Andrej Karpathy](https://twitter.com/karpathy). Although in the README he points to a new, updated and optimized version
called [torch-rnn](https://github.com/jcjohnson/torch-rnn), which I used instead. 

I'm going to skip over the part where it took far longer to get that neural network to run than it should have. I was
installing Torch/Lua for the first time, and they were very uncooperative thanks to some misplaced libraries shuffled
around by the Anaconda package manager, followed by a persistent and unhelpful error. Nothing that a lot of Googling,
re-installing, updating, and banging my head on my desk couldn't fix.

Great, so now I knew how to generate content. But what training data to use? What did I want this bot to emulate?
In the end I settled on two sources that became two different bots (sorry, no universe-mixing): the 7 Harry Potter books
and the currently available 5 books in "A Song of Ice and Fire." When GRRM releases The Winds of Winter somewhere around
2020 (fingers crossed), I might add that one too. In each case, I downloaded the full text files for all books, concatenated
them into two giant text files, and used those as the training sources for each bot. The HP NN (which I'll just call HP) went through 100000 iterations
of training and the ASOIAF NN (henceforth, ASOIAF) did 151850, which took somewhere around 5 and 9 hours, respectively.

After a lot of waiting and a lot of computation, the networks were trained and ready to spit out some sample text. As
it turns out, from an initial observation, ASOIAF performs far better than HP. I think this is partly due to how much cleaner the ASOIAF text file is;
all books were from the same source and from well-formatted pdfs without typos. Some of the HP files included some
strange formatting around the chapter titles and often had a lot of unneccessary punctuation around page breaks and
headings. This causes the HP output text to sometimes start with a string of random punctuation or gibberish in all caps.
In comparison, ASOIAF is far more sensible. I began writing out a more thorough comparison, but I think I'll save that
for a separate blog post, once they've accumulated more tweets.

As for the program to actually send the tweets, that was straightforward. There are plenty of guides out there and the
Twitter API is very well-documented. I set up accounts for both bots, got their API keys and access tokens, and wrote
short scripts to make calls to the Twitter API and write a tweet. There are more lines of code used to set arguments
and call the NN sampler than there are to tweet the output.

The next step is figuring out how to automate it to tweet in set intervals. I briefly looked into Heroku, but haven't had
time to figure out how that would work with all of the torch-rnn files. For now, I made a short shell script to automate
navigating to the python scripts and calling each. I have to manually run it every once and a while throughout the day, but
at least it takes only one line of code.

So now they're up and running! I'm excited to see what they'll produce in the future. As a fun aside, while writing this
post I went looking for examples of other twitter bots (which I ended up not including) and noticed a lot of articles
about a recent bot, [@DeepDrumpf](https://twitter.com/DeepDrumpf), parodying Donald Trump. It turns out that this bot
uses the same NN that I used (well, it used char-nn, so basically the same), but trained on Donald Trump's speeches,
and it was released only about 4 days before I made mine! The results are very interesting, and it's a case where I think the network was used to much greater effect than either
of my implementations, for two reasons: 1) the training data was all dialogue from one person, so using it
as fodder for Twitter posts makes the Twitter bot appear to be that same person, building up the sense of humanness, and
2) Trump's speeches use much simpler language. Both of my bots, just by the nature of their source material being
entire novels, tweet "quotes," which often involve one or multiple characters, dialogue, descriptive words, etc. Keeping
the network to simulating one person makes the results more cohesive and strengthens the illusion that the bot is actually
that person. And the repetition inherent in The Donald's speeches makes the program less likely to generate nonwords,
something that both of my bots are liable to do. Moving forward, I'd like to try and see who might be a good candidate
for a third bot to emulate.