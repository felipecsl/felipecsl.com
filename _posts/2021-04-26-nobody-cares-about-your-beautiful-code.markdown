---
layout: post
title: "Nobody cares about your beautiful code"
date: 2021-04-26 16:26
comments: true
categories:
---

I've recently ran into this tweet from internet famous indie hacker `@levelsio` which went viral and became a Twitter meme of sorts:

<blockquote class="twitter-tweet"><p lang="en" dir="ltr"><a href="https://t.co/LXa46PyeHr">https://t.co/LXa46PyeHr</a> is a single PHP file called &quot;index.php&quot; generating $101,101 this month. No frameworks. No libraries (except jQuery)💖<br><br>(SGD 123.4k=USD 92k) + (USD 9.5k in ads) <a href="https://t.co/jV1gZhyNOM">https://t.co/jV1gZhyNOM</a> <a href="https://t.co/mOlMHvYQws">pic.twitter.com/mOlMHvYQws</a></p>&mdash; ؜ (@levelsio) <a href="https://twitter.com/levelsio/status/1381709793769979906?ref_src=twsrc%5Etfw">April 12, 2021</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

This has mutated into all sorts of ways and turned into a funny meme that made me think more about what's going on:

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">Salesforce made $17 billion in 2020 revenue and is a single php file. No frameworks. No libraries.</p>&mdash; Jon Yongfook (@yongfook) <a href="https://twitter.com/yongfook/status/1382517013327749124?ref_src=twsrc%5Etfw">April 15, 2021</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

And more...

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">Fun fact: Golang is a single PHP file called “go.php”. No frameworks. No libraries (except jQuery)</p>&mdash; Phil Calçado🧶 (@pcalcado) <a href="https://twitter.com/pcalcado/status/1385381381497401345?ref_src=twsrc%5Etfw">April 22, 2021</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

I understand how that might have upset people who in turn make fun of Pieter for his (supposedly) ingenuous tweet. Assuming that the claim is true, how can remoteok.io be so successful and, at the same time, so rudimentar? It seems to go against all the best practices of software engineering that I've learned and followed over the years:

- Package your code down into small, atomic and reusable units
- Follow the [single responsibility principle](https://en.wikipedia.org/wiki/Single-responsibility_principle)
- Use frameworks and libraries to avoid reinventing the wheel
- Whatever language you pick, don't pick PHP 😂
- etc etc..

I could go on and on about all the ways this tweet is an abomination in terms of good engineering standards. I mean, I've always followed these principles myself, including when working on the dozens of side projects that I've dedicated myself to, put it out there to the world and got... zero revenue 😅. Still, Pieter got 100k+ monthly revenue on his PHP monolith. What gives?

Turns out that the harsh truth is...

> Users couldn't care less about the programming language you used or how beautiful, clean, modular and maintainable your code is. In fact, they don't give a crap about it.

This might seem obvious at face value, however, it's in fact very counter intuitive from an engineering point of view. Think about it: All that we've learned about decent, professional level software engineering best practices simply don't apply to early stage startups that are desperately looking for product-market fit. Additionally, anecdotally I can confirm that the vast majority of hyper growth, early stage codebases I've seen and worked on are, putting it nicely, a [big ball of mud](https://en.wikipedia.org/wiki/Big_ball_of_mud).

Out of my last three jobs, all three used Ruby extensively as their primary language to scale up the business. I have strong feelings about maintaining a large scale Ruby codebase. In fact I probably have PTSD from that. Luckily, none of them were in a single Ruby file called `index.rb` (thankfully). Still, all of them were really hard to navigate, maintain and iterate on. This probably deserves a separate article of its own. 😆

Truth is, companies need to make a tradeoff between ["move fast and break things"](https://www.explainxkcd.com/wiki/index.php/1428:_Move_Fast_and_Break_Things#:~:text=%22Move%20fast%20and%20break%20things,highly%20competitive%20and%20complex%20environment.) or grow in a steady, sustainable and healthy pace and be eaten up by competition. In the end, it's all about which startup is able to move faster and adapt quicker until they finally achieve enough traction to then take a step back and reevaluate early technical decisions.

As a result, eventually you reach a point where maintaining that large (usually monolithic) codebase becomes so unbearable, so hazardous that you have to stop and rethink the entire design. I've seen that both at Airbnb and Stripe, both very successful companies, nevertheless. This all comes at a cost, obviously. It all leads to a combination of developer frustration, slower productivity, bugs, incidents, etc. I've experienced it myself time and time again. In the end it's just a tradeoff that companies are willing to make.

Often I see developers that seem to care more about writing clean and beautiful code just for the sake of it, completely forgetting the bigger picture, why they are doing it. I myself honestly probably fell into that trap before, leading to disappointment and burnout. It's the love for the craft that makes us want to do better each day. Still, writing highly clean, reusable and maintainable code is usually not a priority for companies in this category. It's just about shipping, getting the feature in front of users, A/B testing which flow works best, rip apart the failed experiments, rinse and repeat.

> This dynamic creates a weird incentive where, in this environment, developers are rewarded for having a short term mindset focused on shipping more and faster in spite of quality and maintainability.

Ultimately, there is no right or wrong approach, it's mostly just the cost of doing business. If you want to work in a hyper growth environment as a developer, this is price you'll have to pay.
