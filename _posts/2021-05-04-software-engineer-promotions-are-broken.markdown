---
layout: post
title: "Engineering promotions are broken"
date: 2021-05-04 21:10
comments: true
categories:
---

[In my last article](https://felipecsl.com/2021/04/26/nobody-cares-about-your-beautiful-code.html), I briefly covered the misaligned incentives caused by the "move fast and break things" attitude, which causes code quality and maintainability to be an afterthought, incurring additional tech debt and developer frustration. This time, I want to dive deeper into why that happens and how we can fix this perennial issue in the tech industry.

### Engineering levels

Before we begin, we need to briefly talk about the engineering level system. The engineering levels (sometimes called "ladder") framework is a well established process, used by most, if not all, of the biggest tech companies nowadays. I believe it was popularized by the company [Rent the Runway](https://www.progression.fyi/f/rent-the-runway). It was also covered in the book [The Manager's Path](https://www.amazon.com/Managers-Path-Leaders-Navigating-Growth/dp/1491973897), which I'd recommend reading.

In short, the ladder defines a set of levels and traits with different expectations for each level-trait combination, forming a matrix which codifies the expectations for engineers as they progress through their career at a given company. If you're curious, [levels.fyi](http://levels.fyi) mapped out how they compare between companies and is a great resource for understanding the market. As you acquire more knowledge and career experience, you start to "climb the ladder", earning more responsibility and usually getting a pay raise each step of the way. The process of moving up through levels is called a promotion or "uplevel".

If you'd like to read more about it, I'd recommend checking Ben Yolken's [excellent articles](https://yolken.net/blog/stop-hiding-levels) on the topic. Today, I'd like to focus on the levels beyond Senior Engineer, eg. Staff, Principal, Distinguished, etc. and what's wrong with how they currently work. Ben also wrote about the [senior engineer plateau](https://yolken.net/blog/senior-engineer-plateau), which is something I experienced for myself and is tangentially related to this article.

### How I failed to get a promotion

<div class="text-center">
  <img src="/images/2021/05/small-council.webp" alt="Calibration meeting">
  <small>Rare footage taken during a calibration meeting (<a target="_blank" href="https://gameofthrones.fandom.com/wiki/Small_council">source</a>)</small>
</div>
<br/>
The truth is, getting beyond Senior level is actually **pretty challenging**. I've been there. Here's how I failed to get promoted.

Let's give my manager here the fictional name "Bob". This is a true story and happened a number of years ago in a previous job. Bob and I chatted during our 1:1 about what I needed to focus on to make it to the next level. I start working on these things right away, feeling pumped and excited about the possibility of a promotion during the next review cycle. We chat about my progress regularly throughout the year and we both seem to agree that I'm on track. Then, perf season comes around and I carefully write my self review, highlighting my accomplishments, framing them in a way that demonstrates how they match the expectations for the next level. Things are all fine and dandy and Bob tells me I have a really good case for promotion. Now, my destiny is in his hands.

Bob brings my review package to calibration, where my performance is assessed against other engineers by managers and leaders who probably never heard my name and are not familiar with my work. Bob (supposedly) tries to vouch for my work and makes the case for promoting me to Staff level. Something is not quite right though. Charlie, who's a manager in a different org and who has lots of really bright and top performing engineers under him, doesn't seem to agree that my work is up to standards for Staff level. I don't know exactly what happened during calibration though. I wasn't there, plus that's confidential. Bob was representing me, but ultimately the decision was made by a group of people who don't know me, who probably never read my code or even heard about me.

This is how I got disappointed by not getting promoted when I thought that I had a really good case for it. This happened again similarly on the following review cycle, I got frustrated and disappointed again. Eventually, I stopped caring about promotions and just focused on doing my job. A few months later, frustration started building up and I eventually quit. 😂. This problem is not new and has also been illustrated in Michael Lynch's fantastic ["Why I quit Google"](https://mtlynch.io/why-i-quit-google/) article.

You don't have to think too hard to see a lot of problems with the calibration approach. On top of that, add a list of highly subjective expectations for staff engineers and you have a process that ends up being highly arbitrary and decided based on unconscious biases, politics and personal preferences.

> Calibration meetings are ineffective at highlighting engineers achievements since they are not able to advocate for their own work. Performance evaluation for higher levels is often arbitrary and decisions are based on unconscious biases, office politics and personal preferences.

Below are some of the most common traits that are part of performance evaluation for engineers and my observations about each of them.

### Scope and Impact

These are probably the easiest traits to evaluate since it's possible to back up any claims with concrete metrics and data. However, the undesirable side effect of this is that engineers will tend to neglect work that either cannot be easily measured (eg.: refactoring, cleaning up tech debt) or that does not fit into that shape and form that looks good during performance review.

### Productivity, getting stuff done, technical ability

These tend to be more subjective and harder to measure, however it is still possible to have a good sense of how a person is performing by just asking their teammates. One could arguably use metrics like number of merged pull requests, code quality, etc. as a proxy for productivity and technical ability, although I'm not a fan of those. Many of the best engineers I know who were highly skilled and competent didn't necessarily push the most amount of code.

### Visibility, influence and cross collaboration

For staff level and beyond, it is usually very important to demonstrate an ability to collaborate outside of one's own projects, team and sometimes even across multiple organizations. While on the surface that seems to make sense, in practice it's really hard to make a fair judgement about this because, ultimately, it's based on "who knows you". More extroverted and sociable engineers will usually have a head start on this criteria. It also creates a questionable incentive for engineers to over-publicize their work via[ brag documents](https://jvns.ca/blog/brag-documents/), weekly[ 5:15](https://qz.com/work/1516573/the-5-15-is-an-easy-way-to-improve-communication-at-work/)s, shipped emails, regular 1:1s with people outside of their direct team, etc. While some of these practices are probably beneficial for overall communication, they may become a burden and a distraction from focusing on your actual work.

Ultimately, based on my observations, the higher your level, the harder it becomes to accurately judge these traits. The ladder descriptions also seem to get much more vague and it's tougher to have a concrete sense of how to achieve these in practice. It's understandable that companies want to be selective about who to promote, though.

<div style="margin-bottom: 40px">
  <blockquote>
    <p>All these factors combined tend to foster a highly competitive environment where engineers are encouraged to work harder and harder towards a moving promotion target, usually until they eventually burnout and quit.</p>
  </blockquote>
</div>
---

<br/>
Demonstrating the skills, working on the right project and performing at a staff level is not enough, though. As illustrated by my story above, finding a sponsor is likely just as important. Since that person is usually your manager, It’s crucial that you’re both well aligned on your career aspirations. If you really want to dive deeper into this challenge, Will Larson goes into much more depth in his great book [Staff Engineer: Leadership beyond the management track](https://www.amazon.com/Staff-Engineer-Leadership-beyond-management-ebook/dp/B08RMSHYGG).

### How can we fix this?

Getting to staff level shouldn’t be this hard. I believe there is a lot of room for improvement, simplifying and making the requirements clearer and much more objective. It's not entirely obvious how we can get out of this mess, but I have some ideas.

First, I think your teammates, the people who work with you every day and who are very familiar with your work are the ones who are best equipped to vouch for your work. I'd focus a lot more on making peer reviews more useful and constructive.

Second, companies could be run more like DAOs ([decentralized autonomous organizations](https://www.investopedia.com/tech/what-dao/)). A great example here is [MakerDAO](https://makerdao.com/), a decentralized community that uses the [MKR token](https://community-development.makerdao.com/en/learn/governance/mkr-token) for governance. Maker (MKR) holders can [vote](https://vote.makerdao.com/) on proposals using an Ethereum smart contract. These tokens are analogous to shares of a company stock, where shareholders (employees) would be allowed to vote on proposals (eg.: promotions). This would imply that many details that are now private (eg.: compensation, levels, equity distribution) should be made public. Maybe in the future, companies will issue digital tokens on a public blockchain that users and early adopters could buy, instead of the current IPO model. This is already the standard in the [DeFi](https://www.coindesk.com/what-is-defi) space and we have many successful examples like [Uniswap](https://uniswap.org/), [Compound](https://compound.finance/), and [Chainlink](https://chain.link/).

I think this would be a net positive change towards more transparency in the workplace. This is of course not an easy problem to solve and we’re still just scratching the surface of what could be done.

What are your thoughts on all this?

### Acknowledgements

I'd like to thank [Thiago Ghisi](http://thiagoghisi.com/) for reviewing and providing feedback on this article.
