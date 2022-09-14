---
layout: post
title: "Hello Huskly"
date: 2022-09-14 09:23
comments: true
categories:
---

Today I start building Huskly Finance in public. This is something I've been quietly working on during
my free time, just as a hobby, for the past couple of years. The project started as “stocks.dog” but
I’ve since rebranded since that name was temporary and mostly just playful and inaccurate. I’ve been
building it just for myself since it helped me better understand how I was doing as a trader, which
is a skill I’ve gotten more serious about learning and improving since the Covid pandemic started.

Turns out that being a profitable trader is hard. Really hard. I know, quite obvious. This should be
no surprise to anyone, but I decided to learn it the hard way, as I usually do. As I started tracking
my progress more closely with Huskly, I could clearly see which trades worked well and which ones
didn’t. That allowed me to improve my process and have more rigor, keeping myself accountable. As
the saying goes, “what gets measured gets managed”.

![Huskly PnL](/images/2022/09/huskly-pnl.png "Huskly PnL chart")

As this project grew, I started wondering whether other traders could benefit from it and be willing
to pay for it. I still don’t know the answer to that question, but I’m willing to find out. If it
turns out that it doesn’t, at least I know I’ll always have at least one user: myself. 🙂

In a nutshell, Huskly connects with your TD Ameritrade account, which is the broker I currently use.
Your password never hits our servers. Credentials are sent directly to TDA, which sends us a temporary
token (much like a generated one-time password) that allows us to read your account data using their
API on your behalf.

It then imports transaction history daily and reconciles trades, effectively “replaying history” to
figure out what you traded and how much money you made or lost, that is, your P/L. Based on that
information, it generates some fancy charts (like the one above) where you can see your progress over
time, analyze your performance and better understand how you’re doing.

Additionally, there’s a dashboard where you can see your current account positions. It’s focused on
stock options now (which is what I trade mostly), so it shows when it’s in the money, time to expiration,
percent return, etc. I find it quite useful for my own trading so I decided to share this with everyone.

Finally, Huskly can also do charts, with realtime data!

![Huskly Trade Page](/images/2022/09/huskly-trade-page.png "Huskly trade page")

Feel free to reach out via email or Twitter if you want to give it a shot. I’be happy to provide
access to anyone willing to provide feedback in return 😃 It will be most useful if you have a TD
Ameritrade account, though.
