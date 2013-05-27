---
layout: post
title: "More Remote Pairing Tips"
date: 2013-05-09 20:51
comments: false
categories:
- tmux
- remote pairing
- tips
- 3 per week
---

In my latest session of what I am learning I have begun setting up an EC2 instance to handle remote pair programming.  The biggest reason to do this is because it eliminates the need to setup so many little pieces at home.  It seems every remote pair session I start, begins with me explaining the ssh command to login to my laptop only to find that my dynamic dns is changed and ssh doesn't work.  Inevitably I also miss that my router has port forwarded ssh to the wrong machine. Then there is the need to make sure a common user is setup, or that the permissions are setup on the socket that tmux uses.

 >In the classic scream of the 80s: STOP THE MADNESS!!!!!!

If something is painful, stop, evaluate what makes it painful, and find a way to relieve at least some of it.  In this case, that means stop reconfiguring everything each time and do it once on Amazon's EC2 instances.

So now that the mini rant is done, let me point out some great tips on remote pairing.

### Pick a sensible project

If this is the first session you and someone else has ever done.  Don't do serious work. Do a code kata, or pick a code retreat style project. This enables you to focus your attention on how you work together, not the problem you are trying to solve.  Pairing is about communicating, and if you don't give yourself time to learn how each other communicates, you won't solve problems together well. If you don't have one, let me suggest one from my friend [Bill Gathen](http://billgathen.com/ "My #rubyfriend Bill Gathen"). He put together the [7 Degrees of Fizzbuzz](http://billgathen.com/2013/01/18/7_degrees_of_fizzbuzz.html "7 Degrees of Fizzbuzz, learning ruby for beginners, kata for old hands") for the groups he teaches.
 

### Start your tools with vanilla config files

If you both have wildly differing vim configurations and key remappings, only one person will be comfortable driving. Also, the same goes for tmux configs. A remapped leader key kills productivity for the driver.

### Setup your login motd to explain how to get the session started

I can't tell you how well this works to ease the nerves of the begining pair and sets the tone for the rest of the session.

Here's mine as an example

```
  _       _         _                                   
 ( )  _  ( )       (_ )                                 
 | | ( ) | |   __   | |    ___    _     ___ ___     __  
 | | | | | | /'__`\ | |  /'___) /'_`\ /' _ ` _ `\ /'__`\
 | (_/ \_) |(  ___/ | | ( (___ ( (_) )| ( ) ( ) |(  ___/
 `\___x___/'`\____)(___)`\____)`\___/'(_) (_) (_)`\____)
                                                        
                                                                                                              
I'm glad you could join me in my journey of learning Ruby, 
Rails, vim, and tmux. I am still new in so many regards, and 
I welcome your inputs, criticisms, and patience with my knowledge. 
I am sure we will both work well together.

Now that you have logged in, you can join my pairing session 
by typing the following at your prompt:

~~~
tmux -S /usr/local/tmux/learning attach
~~~

Then increase the size of your terminal as far as it can go.
If your screen resolution is larger than 1920x1200 your terminal 
will be filled with dots outside of my screen's resolution.

I tend to tab complete alot.  In Mac terminals this causes a *lot* 
of audible bell sounds. If you want to turn them off, go to preferences, 
Settings, and under the advanced tab, uncheck audible bell.

Happy Pairing!

```
