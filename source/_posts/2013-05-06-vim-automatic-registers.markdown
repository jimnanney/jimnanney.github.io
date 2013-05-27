---
layout: post
title: "VIM Automatic Registers"
date: 2013-05-06 19:48
comments: false
categories: 
- vim 
- 3 per week
---
Vim adventures has taught me an incredible new (to me) trick.  The ability to paste a previously deleted line is easy.  Use **p** or **P** to paste it.  But what if it was the third time you hit **dd** and you wanted to paste in the first thing you deleted.  I cannot begin to count the number of times I needed to do that.  Further down, I'll reveal this secret, but first the backstory:

Recently I saw a link to [Vim-Adventures.com](http://vim-adventures.com/ "Vim Adventures") and followed.  It was appealing, but seemed basic in the first three levels.  So I decided not to purchase the subscription.

And then, at Rails Conf 2013 in Portland, I met up with a friend who was working through one of the levels.  I immediately asked if she was playing vim adventures and she said yes and that she was stuck.  Of course I offered to assist.  This proved several points to me right away.

> First, I am not as good with VIM as I had thought.

> Second, I am a horrible teacher of things I have little grasp on.

> Third, Vim Adventures advances terribly quick after level 3 and is well worth the subscription.

It was inevitable afterwards that I subscribed.  I have learned a ton, and the most profound ended up being the automatic buffers.

Here's how they work:

Given these lines:
```
Delete me last.
Delete me third.
Delete me first.
```

If you delete line three by using **dd**, followed by line one with another **dd** and then line two with again a **dd**, several deletion registers would be created.

You can see these by typing **:reg**

First, notice they are numbered from **"1** to **"9** and that they are in order from first in to last in. They also rotate out as more are added.

So to paste the first deletion from above, you would use **"3p**

This simple thing has bothered me many times, but not enough to look it up. After playing vim adventures to level 10, I've learned this new trick.

