---
layout: post
title: "Getting Started with Vim"
date: 2013-06-27 13:26
comments: true
categories: text editors, vim
---

Let me preface this post by saying I have frequently gone back and forth
between vim and Sublime-Text-2. I have also experimented with other
editors such as Text-Mate and Emacs but vim keeps drawing me back. There
are three main reasons why I love vim so much. 

First, it's fast, mindblowingly fast. Not just the actual program but
the speed of editing as well.

Second, it's open source. This one is more of a personal thing. I love
open source projects and while Sublime and TM are both great editors,
they're not open source.

Third, it has a ton of modules and extentions. Vim has been around for
over 20 years and in those 20 years developers who love to develop in
vim have made it better and better. Almost any functionality you could
possibly want from vim you can find someone who's already written a
plugin for it.

Getting started:

The first time I opened up vim I had no idea how to write any text and
it took me five minutes to quit the program. I had no idea how to use it
and thought I could learn it like many other pieces of software, just
diving in. Vim is less complicated that it seems at first but it still
acts like no other text editor you've used before. The most simple and
painless way to get a handle on the basiscs is to run
<code>vimtutor</code> 
from the command line. This will go through basic commands and
navigation. Once you learn how to navigate vim with the keyboard you'll
never touch your mouse again. Mice are a slow way to interact with your
computer. Even with a high sensitivity it requires a lot of movement to
accomplish the same thing as a few keystrokes.

Now, if this entire blog post just said "go run vimtutor, the end." That
would be a pretty useless blogpost. So, here's where I get into my
advice on how to actually learn vim: start small. After you run through
the vim tutor, try using Sublime-Text in "vintage mode." Instructions
for setting that up can be found <a
href="http://www.sublimetext.com/docs/2/vintage.html">here</a> It's a
great way to get started using vim-like commands while still having
access to more traditional text-editor features. After you get sublime
running vintage start picking a single key or set of keys to learn each
week or each day or some other arbitrary amount of time. For isntance
your first day, don't use the mouse to navigate your text. Use the
"hjkl" keys instead. Once you're compfortable with that, start using the
"{}" keys to navigate. Just keep adding new keys to your bank of muscle
memory. If you do somethign in sublime frequently using ctrl shortcuts,
see if there's a way to do it using vim shortcuts. Every time you use
your mouse, look up a way to do that same action from the keyboard. 

Once you get comfortable in vintage mode, start using the command line
vim to edit single documents. This is a lot simpler than trying to edit
a structured app like a Rails app. After you get used to that, learn
some new commands and get comfortable, try some third party software. If
you're a rails developer I highly reccomend <a
href="https://github.com/carlhuda/janus">Janus</a> it has almost every
additinal plugin you could want and makes it easy to install the ones
that it doesn't include. 

Long story short, start small with vim. It's a very complex text-editor
that you could spend years learning to master but as you learn, you'll
find your coding workflow getting faster and faster.
