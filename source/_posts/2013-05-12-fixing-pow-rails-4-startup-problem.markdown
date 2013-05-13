---
layout: post
title: "Fixing Pow Rails 4 Startup Problem"
date: 2013-05-12 14:50
comments: true
categories: 
---
I just had an interesting problem trying to use pow for a Rails 4 project for the first time.

Pow was reporting an error parsing the following line in  **config/application.rb**

```
config/application.rb:11: syntax error, unexpected ':', expecting ')'
Bundler.require(*Rails.groups(assets: %w(development test)))
```

That error message really looks like Ruby 1.8 trying to parse the new hash syntax. And in fact that is exactly what it is.

It turns out that I had RVM configured wrong.  I use zsh and in my .zshrc I had the startup for rvm.  If the rvm script doesn't get called the default system ruby is used with pow.  In the case of pow, it never loads the .zshrc because that is only called for interactive environments. The solution is to move the lines that call rvm from .zshrc to a new or exisiting .zshenv. Once you do this you will have to kill the exisiting pow process **ps ax |grep pow**

I really love using pow during development as it allows me to completely ignore the localhost:3000 and 5000 and other ports and can load the app in my browser by name instead.

You can find pow and the documentation from [Pow.cx](http://pow.cx "Pow.cx").

