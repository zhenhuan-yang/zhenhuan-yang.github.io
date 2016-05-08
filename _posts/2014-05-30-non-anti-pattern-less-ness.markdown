---
layout: single
title: "Non-Anti-Pattern-Less-Ness"
modified: 2014-05-30 15:43:01 -0400
categories: writing
excerpt:
tags: [pattern, random, information]
image:
  feature:
share: false
date: 2014-05-30 15:43:01-0400
---
In drafting my proposal to present in the TEDxGallatin Senior Symposium, I found myself agonizing over the fact that there isn't a single satisfactory antonym for the word pattern. Always quick on his feet, Red Flag pointed out that there isn't a single satisfactory antonym for most things. "What's the opposite of a cat? Or a rumba? Or playing cricket?" Exasperated, I had to admit that he was right. I frowned and contemplated. Someone suggested _chaos_, but chaos is a more appropriate antonym for order, which isn't quite what I mean by pattern.
 
By pattern I mean a simplified representation of a system that, despite its simplicity, retains all the relevant information about that system. So let's say for example that I wanted to send you the first 100 numbers of the Fibonacci sequence. I could send you the following:

> for n → 100: F(0) = 0, F(1) = 1, F(n) = F(n - 1) + F(n - 2) for n ≥ 2

which is considerably more compact than writing out the first 100 numbers of the Fibonacci sequence, and yet you get all of the information you need! Furthermore, bona fide chaos is impossibly, wonderfully pattern heavy.

It ultimately occurred to me that there not being a satisfactory antonym for pattern reveals something rather fundamental about non-patterns. Any term would require some method of determining which things count as members and which don't. If I could come up with a decision procedure for non-pattern-ness, it would point to there actually being a pattern to non-pattern-ness!

This re-routed me to a very difficult point from _GEB_ that I'm still trying to wrap my head around: that there are formal systems whose negative space is not the positive space of any formal system. It's hard to communicate the weight of this point in less than 800 pages (I joke that all I want in life is the DH advantage of having 500+ pages to say any- and everything I want and need to say), but I'll do my best.

Let's take the Fibonacci sequence to be the formal system we're concerned with; Fibonacci numbers make up the positive space of this formal system, and non-Fibonacci numbers make up the negative space. Let's say I want to know if some random number is a Fibonacci number. I could, of course, write out the Fibonacci sequence from the beginning until I either arrive at or pass the number. However, the bigger the number, the longer this process will take, and the greater the chance of it not being a Fibonacci number and thus the greater the chance of me having wasted my time. It would be nice if there was a test that I could perform on any number that would tell me whether or not that number was a Fibonacci number. Such a test is what DH calls a _decision procedure_, and it will tell me whether or not a number falls into the positive or the negative space of my formal system. If it falls in the positive space, it's a Fibonacci number; if it falls in the negative space, it's not.

If you're feeling dangerous, it might occur to you to ask if there is a complimentary decision procedure for non-Fibonacci numbers, a test that would tell you if a number is not a Fibonacci number. Of course, this information is implicitly encoded in the negative space of our formal system + decision procedure, but what if I was particularly interested in flipping everything around so that the positive space became the negative space, the negative space the positive space? Is the new positive space a formal system in the same way that the old positive space was the Fibonacci formal system? Is there a decision procedure that determines which numbers count as part of this system and which don't?

In other words, do their boundaries "touch", does the positive space infer the negative space, and the negative space the positive space? For some formal systems, the positive space and the negative space both have their own rhyme and reason. However, there are some formal systems where the boundaries don't touch in this way. The relationship between members and non-members of the formal system is more complicated.

With respect to patterns and non-patterns, it seems that pattern-ness and non-pattern-ness are in just such a complicated relationship. The negative space of pattern-ness—i.e., non-pattern-ness—cannot, by definition, have a decision procedure. Non-patterns cannot be the positive space of their own formal system because to be so would require such a decision procedure.

My intuition is that having a pattern that represents the system and having a decision procedure for identifying members of the system are two very closely related features of formal systems, but I have nothing really to say about this at the 
moment. Randomness, I finally had to admit, is the best candidate for an antonym to pattern because there is no simplified representation of a random system that retains all of the relevant information, and _non-pattern_ doesn't capture the complicated boundary between patterns and non-patterns. I do wish "random" could be a noun, though.

Red Flag agreed, and added that a count noun would be especially nice. "Was there any connection between the asteroid that passed by Earth and the meteorite in Russia?" "Nah, it was just a random."

Despite my linguistic difficulties, my proposal made it past the first round, and I have an interview on Thursday. Wish me luck!
