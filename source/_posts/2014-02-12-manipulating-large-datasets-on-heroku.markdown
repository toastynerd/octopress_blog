---
layout: post
title: "Manipulating Large Datasets on Heroku"
date: 2014-02-12 19:13
comments: true
categories: 
---

The majority of Rails developers I have met have used Heroku at some point during their career. 
Heroku boasts many strenghts, a free tier, command line tools and it supports Rails out of the box.
I can think of no easier way to deploy small, simple Rails sites than with Heroku. Hell, this blog 
is currently hosted Heroku.

The downside comes when things start to get big or complicated. Heroku doesn't provide many easy ways
to deal with large data sets or custom architecture and tools. At least not in a way that's cost 
effective. Which, when you're working at non vc-backed startup is more than just a passing consideration.
It's doable but it takes a little bit more effort.

One of the big limitations of Heroku is the memory limit. Heroku 1x Dynos run on Amazon Web Services
micro instances and have a memory max of 512mb. The 2x dynos have twice as much ram but they cost 
twice as much and can get extremely expensive to keep on.
