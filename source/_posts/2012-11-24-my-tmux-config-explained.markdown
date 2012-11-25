---
layout: post
title: "My tmux config Explained"
date: 2012-11-24 23:42
comments: true
categories: 
---

Before I get too far into my posts on pairing I wanted to start adding my configuration files and why I have chosen to use the pieces in them.

I must admit that prior to this week I had never used tmux.  I heard the ruby rogues talk about it on their podacst. However, being a previous Linux admin, I have used and taught others to use screen for any task that was important, or long running.  Largely due to the simple fact that a session could be detached and reattached.

Tmux is like screen on steroids.  I have never used panes within screen and tmux makes this easy to do.  With a few customizations it is incredibly useful, and your fingers rarely leave the home row on a keyboard!

<!-- more --> 
So before I break out the sections of my tmux.conf, I'll present it in its entirety here.  As an aside, each of these things I got from Brian P. Hogan's book called ["tmux: Productive Mouse-Free Development"](http://pragprog.com/book/bhtmux/tmux). (Not a referral link)

{% gist 4142309 %}

Firstly, in screen every command is prefixed with Control A.  Tmux uses Control B.  I remap it to Control A and unbind the original Control B.  This is also very useful if you remap your caps lock key to control as then your fingers do not leave the home row.

{% codeblock Remap Prefix to Control-A %}
set -g prefix C-a
unbind C-b
{% endcodeblock %}

Next I set the escape detection time low to avoid conflicts with vim.  Further detail on this can be found in Brian P. Hogan's book, but trust me, if you use vim in a tmux session, you'll want this.

{% codeblock Fix Escape Detection %}
set -s escape-time 1
{% endcodeblock %}

These next two are convenience only and should make VB programmers happy :P  All they do is set the start value of the numbering schemes for windows and panes to 1 instead of 0.

{% codeblock Renumber from 1 %}
set -g base-index 1
set -g pane-base-index 1
{% endcodeblock %}

Next while editing the tmux.conf file I want to be able to reload it with a shortcut key instead of `C-A :` followed by typing `source-file ~/.tmux.conf`

{% codeblock Reload %}
bind r source-file ~/.tmux.conf\; display "Reloaded!"
{% endcodeblock %}

I also don't want to remap away C-A from whatever programs I am using.  So I hit C-A twice and it gets sent to the underlying program instead of tmux with the following.

{% codeblock Send C-a to program %}
bind C-a send-prefix 
{% endcodeblock %}

Tmux lets you split a window into panes horizontally and vertically with `C-a %` and `C-a "`  But the pipe and dash are more intuitive.

{% codeblock More intuitive Window Pane Splits %}
bind | split-window -h
bind - split-window -v
{% endcodeblock %}

Now for the fun stuff.  I use vim constantly.  I am not good at it, but I use it nonetheless.  I want to move around the panes using vim's movement keys.

{% codeblock Use vim's h j k l movement keys %}
bind h select-pane -L
bind j select-pane -D
bind k select-pane -U
bind l select-pane -R
{% endcodeblock %}

Switching windows should be the same way, using vim's h and l movement keys. The -r makes it repeatable without having to press C-a again.

{% codeblock Use vim's h and l to switch windows %}
bind -r C-h select-window -t :-
bind -r C-l select-window -t :+
{% endcodeblock %}

Let's now add vim movement key emulations that go to resizing a pane.  The defaults are C-Arrow keys, but this isn't home row friendly.  Again notice the -r. And also notice that the movement keys are capitalized.

{% codeblock Resize from home row keys %}
bind -r H resize-pane -L 5
bind -r J resize-pane -D 5
bind -r K resize-pane -U 5
bind -r L resize-pane -R 5
{% endcodeblock %}

Now some of you are faster typists than I and won't need this.  But I don't want to repeat the C-a while resizing and I may pause less than a second to see the change.  This 1000 represents 1 whole second to repeat my last keystroke.

{% codeblock Longer delay for allowing a repeated keystroke %}
set -g repeat-time 1000
{% endcodeblock %}

Next is the colors, which I'll leave for you to get your own color schemes.  I am definitely not a designer.

Lastly when in the scroll mode which allows copy and scrollbuffer movement, I want to use the vi keystrokes to navigate the scrollbuffer.

{% codeblock Scroll Buffer Movement like Vim %}
setw -g mode-keys vi
{% endcodeblock %}

And that is the end of my .tmux.conf explanation.  These will get you moving like vim and splitting panes all over the place.  Enjoy!


