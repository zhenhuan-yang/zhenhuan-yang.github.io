---
layout: single
title: "Upstart and Algorithms of Exclusion"
modified:
categories: writing
excerpt:
tags: [algorithms, bias, lending, startups]
image:
  feature:
share: false
date: 2015-08-05T17:16:01-04:00
---
On July 27th, the New York Times published an article about algorithms that “determine character” titled, you guessed it, _Determining Character With Algorithms_[^1]. The article highlighted Upstart, a loan-lending startup that aims to supplement credit history with transcripts and standardized test scores to create a picture of credit for people that don’t have the credit history, good or bad, that comes from having a few credit cards and a mortgage. The idea is that your standardized test scores, which college you attend, your major, and your GPA indicate how important you feel your sense of obligation to repay a loan would be if you were given one. In short, Upstart is concerned more with your “willingness” to pay back a loan than your ability to pay back a loan, and it uses your transcripts and standardized test scores to determine how willing you are.

While the article focuses on loans, there’s a nice shoutout to criminal risk assessment, because we all know that that’s not [hugely problematic](http://mathbabe.org/2014/08/12/weapon-of-math-destruction-risk-based-sentencing-models/). The article alludes to data validating the claim that students with higher GPAs are more likely to repay their debts, but that wasn’t enough to be going on for me to find it. What’s troubling about this article—and about the Upstart lending model—is that it fails to acknowledge the disparate factors that can and do impact GPA, standardized test scores, and college acceptance.

A 2002 study by Jay Rosner showed that sample questions which were answered correctly by more African-American students were not included in the tests. They were excluded so that test results showing African-Americans scoring lower than whites would be, wait for it, _consistent_.[^2]

_The Chosen: The Hidden History of Admission and Exclusion at Harvard, Yale, and Princeton_ by Jerome Karabel examines the transition of the Harvard, Yale, and Princeton admissions processes in the 1920s from an exam-based system, in which anybody that passed the exam was admitted, to an entirely new system “with [an] emphasis on such things as character, leadership, personality, alumni parentage, athletic ability, [and] geographical diversity.”[^3] (Notice that key word, “character”.) The transition was introduced to address the problem of two many of the “wrong students”—namely, Jewish students of Eastern European background—passing the admissions exam and gaining acceptance. Admissions processes have changed over time, but the problem remains: acceptance criteria, especially for elite institutions, are rigged to favor the qualities that the elite and their children are most likely to possess.

A lot of students (including me) work while they’re in school, and there are different contexts in which they do so. Some students work to cover the costs of attendance; others work to explore career options or gain experience. “Regardless of the reason for working, trying to meet the multiple and sometimes conflicting simultaneous demands of the roles of student, employee, parent, and so on often creates high levels of stress and anxiety, making it less likely that students will complete their degrees.”[^4] Take a related example from my field: one of the recognized forms of child neglect is educational neglect. A child can become a victim of educational neglect if, say, their single parent has to work and they have to stay home to watch their younger sibling. You could argue that staying home to take care of your younger sibling, or finding and holding down a job in college to cover your expenses—even at the expense of your GPA—could indicate how important you feel your obligations are, or, how “willing” you are to fulfill your obligations.

Lending is a thing that I don’t know a whole lot about, but I do know that it’s against the law for creditors to discriminate against applicants based on race.[^5] If class is a shadow cast by race, is discriminating based on class—and make no mistake, that *is* what we’re talking about—any more legal? If your algorithm doesn’t explicitly address socioeconomic disparities in the factors it uses to make predictions and determinations, not only is it biased, it is just making it easier to enforce and perpetuate those disparities.

Lucky for us, Jure Leskovec, a professor of computer science at Stanford University, is here to tell us that “Algorithms aren’t subjective. Bias comes from people.” This article barely takes the bait, counterarguing that yeah, but algorithms are designed by people and people are biased. And by “barely” I mean two sentences. In a true feat of comedy though, the article nonetheless manages to expose the very problem of biased people developing biased algorithms that the author refused to actually deal with. At the beginning, the articled quotes the founder of another company targeting “subprime borrowers” as saying:

> “We’re always judging people in all sorts of ways, but without data we do it with a selection bias. We base it on stuff we know about people, but that usually means favoring people who are most like ourselves.”

And then at the end, the article echoes Paul Gu, one of Upstart’s co-founders, saying that he wouldn’t have qualified for one of Upstart’s loans under the company’s initial algorithms. They’ve since changed the design. Doesn’t that sound eerily like “favoring people who are most like ourselves”?

What’s concerning about these types of algorithms is that they make the perpetuation of social biases and class easier, more efficient. What’s concerning about the attitude about algorithms and data expressed by the author and those quoted in this article is the righteousness they feel while perpetuating injustices with greater ease and efficiency.

[^1]: The story appeared online on July 26th with the title _[Using Algorithms to Determine Character](http://bits.blogs.nytimes.com/2015/07/26/using-algorithms-to-determine-character/)_.
[^2]: Kidder, W. C., & Rosner, J. (2002). How the SAT Creates Built-in-Headwinds: An Educational and Legal Analysis of Disparate Impact. _Santa Clara L. Rev., 43_, 131.
[^3]: Schatz, R. D. (2005). How Harvard, Princeton, and Yale Restricted Jews, Smarties, Blacks. _Bloomberg_. Retrieved from http://www.bloomberg.com/apps/news?pid=newsarchive&sid=a77U1Kc6qakI
[^4]: Perna, L. W. (2010). Understanding the working college student. _Academe, 96_(4), 30-33.
[^5]: Equal Credit Opportunity Act 15 U.S.C. § 1691

