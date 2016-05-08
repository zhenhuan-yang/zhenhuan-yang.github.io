---
layout: single
title: "The Ban and the Bit: Alan Turing, Claude Shannon, and the Entropy Measure"
modified: 2014-06-14 15:54:12 -0400
categories: writing
excerpt:
tags: [Cold War, information, cryptography, entropy, Claude Shannon, Alan Turing, mathematics, information theory]
image:
  feature:
share: false
date: 2014-06-14T15:54:12-0400
---
> “I didn’t realize [Turing] was as important as he was.” — Claude Shannon[^1]

In late 1945, as World War II was drawing to a close, John von Neumann began assembling a small group of engineers at the Institute for Advanced Study (IAS) at Princeton to design, build, and program an electronic digital computer. In the spring of that year, von Neumann had visited Los Alamos (specifically, the target selection committee of the Manhattan Project, the group responsible for choosing the first targets of the atomic bomb) to oversee computations related to the expected size of atomic bomb blasts, estimated death tolls, and the distance above the ground at which the bombs should be detonated for maximum effect (Rhodes, 1986). When von Neumann arrived at the IAS, his focus had shifted. “I am thinking about something much more important than bombs,” he remarked in 1946. “I am thinking about computers” (Dyson, 1981, p. 194). Ten years later, von Neumann died, leaving his pioneering volume The Computer and the Brain unfinished. There are only two names mentioned in the volume: Alan Turing and Claude Shannon.

Alan Turing was a British logician and cryptologist, celebrated for cracking the German Naval Enigma code during World War II at the Government Codes and Ciphers School at Bletchley Park, UK. “The scientific triumph at Bletchley—secret for the duration of the war and for thirty years after—had a greater effect on the outcome than even the Manhattan Project, the real bomb.” (Gleick, 2011, Loc 3436) Turing is also widely considered to be the father of both computer science and artificial intelligence (AI). The electronic digital computer that von Neumann’s group built at the IAS was the first physical realization of a Universal Turing Machine, a theoretical machine proposed by Turing in 1936.[^2]

If information and communication were as “exciting” as computation and AI, perhaps Claude Shannon would be as famous as Alan Turing. In fact, upon consideration of the totality of Shannon’s work, it may not be an overstatement to say that he was the father of the Information Age we find ourselves in today. Shannon is best known for introducing the concept of entropy as a measure of information. This idea was first introduced by Shannon in a classified report written for Bell Laboratories in 1945 titled _A Mathematical Theory of Cryptography_. The report was declassified and published in the Bell System Technical Journal in 1949 under the title _Communication Theory of Secrecy Systems_, one year after Shannon published his seminal paper _A Mathematical Theory of Communication_, also in BSTJ.[^3] The following year, MTC would be joined by an essay by Warren Weaver and published (with a grander first word) as _The Mathematical Theory of Communication_ (Shannon & Weaver, 1949).

In MTC, Shannon set forth a definition of information that was central to his entire theory of communication. According to Shannon, the information content of a signal can be measured as the average unpredictability in a random variable. Consider a deck of cards that are in order. As you flip each card over, you don’t get very much new information because you can predict what each card is going to be. But if you shuffle the deck, you get more information as you flip each card over because you can’t predict what each one is going to be. For Shannon, the information in a signal is altogether separate from the meaning of the message. “The semantic aspects of communication are irrelevant to the engineering problem. The significant aspect is that the actual message is one _selected from a set_ of possible messages.” (Shannon, 1948, p. 5, Shannon’s emphasis) Information, Shannon realized, wasn’t intrinsic to the random variables, i.e., the cards, but to how disordered they were.

Recognizing the analogy to statistical mechanics and thermodynamics, Shannon called the disorder of a system its entropy. To measure a system’s entropy, Shannon defined the basic unit of information as a signal representing one of two possible states. For example, one unit of information is the amount of information contained in a single coin flip. Information, Gregory Bateson (1979) said, consists in “a difference which makes a difference” (p. 99).

But according to Good (1950, 1979), Turing had already introduced entropy as a measure of information—in 1940.[^4] Good’s (1950) references to Turing and entropy in his book Probability and the Weighing of Evidence are oblique at best. This is to be expected considering the book was published at a time when the work being done at Bletchley Park (and at Bell Laboratories, for that matter) was heavily classified. By the end of 1939, Turing had successfully cracked the German Naval Enigma system[^5], but it was of the utmost importance that this information remain secret, especially from the Germans, and though Shannon’s cryptography paper was declassified and published in 1949, both his and Turing’s work on cryptography at the end of World War II and through the beginning of the Cold War remained classified until 1974, 20 years after Turing’s death in 1954.

Shortly after secrecy was lifted, Good (1979) published a paper on Turing’s work during 1940 and 1941 titled _Studies in the History of Probability and Statistics_. In this paper, Good (1979) gives an account of Turing’s contributions to statistics while working at Bletchley Park that were never published. Good makes it clear that Turing had introduced the concept of entropy with respect to information at least two years before he came to Bell Laboratories in 1943.

As the veil of secrecy was pulled back, a question emerged: did Turing give Shannon his most famous idea when they were at Bell Laboratories together? On 28 July 1982, 26 years after Shannon had left Bell Laboratories, communication engineer Richard Price asked him this precise question:

> I thought I might come over tonight being able to tell you that secrecy was now lifted and you could talk freely about what Turing told you. And it’s only the past couple of days that I’ve been told that you never had the need to know in the first place, so Turing would never have been able to tell you this. So I had the notion that perhaps since Turing had already come up with the entropy measure in the context of cryptography in 1940, that again that might have been a lead-in to you, because it is known that he got together with you. (Price, personal communication, 28 July 1982)

Shannon denied the suggestion flat out. “Not at all. [...] We talked not at all about cryptography. Now I don’t think we exchanged one word about cryptography. We talked much more about things like the human brain and computing machines and that sort of thing.” (Shannon, personal communication, 28 July 1982) Price is incredulous, but Shannon insists.

> Price: OK, well that...

> Shannon: That kills that theory. (Price & Shannon, personal communication, 25 September 1982)

World War II brought important advances, but the field remained a kind of technological archipelago, with several islands of knowledge that didn’t talk to each other. Radar, developed during the war, was still a secretive subject. The telephone system was operated almost entirely by AT&T. At universities, communication engineering textbooks amounted to the impressive quantity of two; students learned radio transmissions and technologies such as AM and FM. Communication had advanced significantly during wartime, but it was far from a unified science. (Guizzo, 2003, p. 28)

There was a duality at play between Shannon and Turing and their wartime cryptography work.[^6] While Turing was at Bletchley Park decoding intercepted messages from the Germans, providing Churchill with invaluable information, Shannon was at Bell Laboratories working on the X System, an encrypted telephone system used by Churchill and Roosevelt to conduct transoceanic conferences.
Shannon was working on concealing information on the one hand while trying to transmit it on the other hand, and he got the idea for his theory of communication while working on the encryption scheme for the X System. “He realized that, just as digital codes could protect information from prying eyes, so could they shield it from the ravages of static or other forms of interference.” (Horgan, 1992, p. 74) In working on his 1945 cryptography paper, Shannon realized that digital codes could be designed to package information not only more efficiently (so that more information could be transmitted over a given channel), but they could also be designed to make them unbreakable. (Shannon, 1949) “While in cryptography you want to protect a message from eavesdroppers, in information you want to protect a message from transmission errors. In both fields you need a measure of information and you deal with [en]coding and decoding methods.” (Guizzo, 2003, p. 20) It would turn out that these both involved the same thing, entropy, which would become the foundational piece of Shannon’s information theory.

Shannon defined the basic unit of information as a signal representing one of two possible states, such as the flip of a coin. Systems with two possible states are generally referred to as binary systems. In binary notation (usually comprising 0s and 1s), a signal can be communicated by a single digit in virtue of the fact that there is an alternative to it. The fact that you can communicate with one digit because there are two possible digits is central to information theory. John Tukey invented the term “bit”—a contraction of “binary digit”—in 1947, and this was the term that Shannon adopted as the unit of information.[^7]

Several years before, in 1940 or 1941, Turing had invented the term “ban” as a unit of information. (Good, 1979, p. 394) Unlike a bit, which corresponds to the amount of information in a signal in a binary system, a ban corresponds to the amount of information in a signal in a decimal system. According to Good (1979), “Turing was the first to recognize the value of naming the units in terms of which weight of evidence is measured. [...] It was much later that a unit of information for base 2 was called a bit and the same units can be used for information as for weight of evidence” (p. 394).
Not only did Turing recognize the significance of being able to quantify (i.e., measure) information, he also recognized that measuring information was a matter of measuring the unpredictability of a random variable, what he and Good (1950, 1979) refer to as “the weight of evidence”. In chapter 6 (Good, 1950), a † in the following sentence directs the reader to a footnote containing a citation of Shannon’s MTC: “While the manuscript was with the publishers an article appeared† involving ideas that are related in some ways to those of the present chapter.” (Good, 1950, p. 74) This is the first sentence of the last section of the chapter, under the heading “6.9 Entropy”. Importantly, the section ends with seven remarks of Shannon’s—not Turing’s—on entropy as a measure of information. (p. 75)

In 1943, before Shannon wrote his paper, Turing was invited to Bell Laboratories to consult on cryptography, and the two met often. “Not a huge amount,” Shannon recalls, “but quite a bit” (Shannon, personal communication, 28 July 1982). But because Turing was decoding and Shannon was encoding, they were kept separate professionally. As Price reveals above, and Shannon reiterates throughout his interview, Shannon was unaware of the work that Turing was doing, both at Bell Laboratories and at Bletchley Park.

> Price: You sensed that when [Turing] came over here [...] you sensed that he was up to very important war business?

> Shannon: I had no concept of the Enigma machine, is that it? I didn’t know of that nor that he was a crucial figure in it. No.

> Price: You knew of other people that you inferred were interested in cryptography, but you didn’t even know he was interested in it.

> Shannon: Oh, no, I knew that he was interested in it, and I thought he was working—

> Price: Cryptography?

> Shannon: In cryptography, yes.

> Price: You knew that much?

> Shannon: I thought that, yes. Or I don’t, didn’t, wouldn’t say I knew it, but that was my understanding. But I didn’t realize that he was as important as he was.

> Price: That was a question you didn’t want to ask him, I suppose. Having guessed that he was in cryptography, you wouldn’t want to ask that question?

> Shannon: No.

> Price: Right, because it was too sensitive to ask, perhaps?

> Shannon: Well, in the wartime you didn’t ask too many questions. (Price & Shannon, personal communication, 28 July 1982)

It seems unlikely, given how closely related their work was to each other’s, that Shannon and Turing never “compared notes” as Price (personal communication, 28 July 1982) put it. Indeed, Price borders on incredulous about this point throughout the entire interview. However, he does say that John Tukey and William Bennett—both of whom were at Bell Laboratories with Shannon and Turing—confirmed that Turing wouldn’t have said anything to Shannon about the cryptography work that he was doing. (Price, personal communication, 28 July 1982)

Even considering Good’s (1950, 1979) claims about Turing’s introduction of the entropy measure, the literature seems to support Shannon’s repeated claims that Turing didn’t tell him about it. Shannon is mentioned twice in Good’s (1950) book and once in Good’s (1979) paper; three times in Copeland’s (2004) book The Essential Turing; and seven times in Dyson’s (2012) book Turing’s Cathedral. With the exception of Good (1950, 1979), each mention is in reference to computer chess or AI. 

Conversely, Turing isn’t mentioned, in the text or in the references, in a single paper of Shannon’s on communication theory, information theory, or cryptography, but he is mentioned in several of Shannon’s papers on computers, circuits, and games. (Sloane & Wyner, 1993) This agrees with Shannon’s claims about what he and Turing talked about when they were together (Shannon, personal communication, 28 July 1982), and the testimony of Tukey and Bennett only strengthen Shannon’s claims.

On 25 September 1980, at the third World Computer-Chess Championship in Linz, Austria, Claude Shannon gave an interview to H J van den Herik (1989). Unsurprisingly, the interview centered around the topic of computer chess, and AI more generally. However, Shannon does mention his and Turing’s work on cryptography at Bell Laboratories:

> van den Herik: You and Turing were working in [computer chess] at the same time, but in the literature there is no sign that you have ever met each other.

> Shannon: We have met each other. He visited the Bell Laboratories, where I was working, during World War II for quite a period of time. Turing at that time was interested in cryptography and secrecy systems. He was working for the government, I believe. I was too, but as a matter of fact we couldn’t even talk about that subject to each other because it was such a highly classified subject. He was contacting certain people at Bell Laboratories and I was contacting others. But we did meet a lot and talked about things. He was very interested in what you could do with a brain, how a brain could be made mechanically, as I was, and we discussed that a great deal. We talked a little about chess-playing machines. Later I went over to England, about 1950, and among other things I visited a conference on information theory there, and Turing was there too. Then I went over to Manchester and there was a computer. He was trying to program it for chess, he and Good, and we discussed these problems.

> van den Herik: From a later point of view it seems that your ideas and those of Turing had the same origin.

> Shannon: We certainly discussed those things to some extent, earlier. It is hard to say with things like that; sometimes they are, as we say, in the air, if one person doesn’t do it somebody else will. (p. 221–222)

What “ideas” is van den Herik asking about? What “things” is Shannon talking about, his and Turing’s ideas about computer chess, or their ideas about cryptography and secrecy systems? It’s questionable.[^8] The following exchange between Shannon and Price (1982) seems to offer the most insight into the issue:

> Shannon: “I had talked to [Turing] several times about my notions on Information Theory [...] and he was interested in those.

> Price: Can you remember any feedback he might have given you on that?

> Shannon: He was interested. He somehow didn’t always believe these...my ideas...he didn’t believe they were in the right direction. I got a fair amount of negative feedback. (Price, Shannon, personal communication, 28 July 1982)

Indeed, Turing never did publish anything on the entropy measure, and it seems he tried to discourage Shannon from doing so as well. But why? There are two possibilities. The first is that Turing, for whatever reason, didn’t believe that the entropy measure was something worth pursuing. The second is that Turing did believe that it was something worth pursuing and intended to publish his own work on it, but died before he was able to do so (i.e., before the veil of secrecy was lifted). Either way, Turing wouldn’t have had a reason to give Shannon the idea. As Shannon said, “sometimes [these things] are, as they say, in the air” (Shannon, personal communication, 25 September 1980).

***

_Researching this question has been a particularly challenging and intriguing task. There are five biographies of Alan Turing, and not a single biography of Claude Shannon. Thus, stitching together an account of Shannon’s intellectual trajectory consists in careful readings of his own published work, his interviews, and his appearance in works about other people’s lives._

[^1]: Shannon, personal communication, 25 September 1980. See van den Herik, H. J., & Shannon, C. E. (1989).
[^2]: See Turing, 1936
[^3]: These two papers will be referred to throughout as the “cryptography paper” and “MTC”, respectively.
[^4]: See Good, 1950, p. 63
[^5]: See Copeland, 2004, p. 341
[^6]: If there is a single name associated with cryptography during and immediately after World War II, it’s Alan Turing, not Claude Shannon. This is something of an unfair characterization of the wartime cryptography considering that in his cryptography paper, “Shannon [...] gave cryptologists what they had never before possessed: a rigorous way of assessing the security of any secrecy system” (Gleick, 2001, Loc 3499). Shannon did nothing short of turning the art of cryptography into a science.
[^7]: Interestingly, in 1936, Shannon’s mentor (and director of the National Defense Research Committee) Vannevar Bush had written of “bits of information” that could be stored on the punched cards used in the mechanical computers of that time. See Bush, 1936, p. 653.
[^8]: Turing isn’t mentioned again in the interview. This is surprising given that van den Herik’s very next question is: “what do you consider as milestones in the field of Artificial Intelligence as a whole?” (van den Herik, 1989, p. 222).