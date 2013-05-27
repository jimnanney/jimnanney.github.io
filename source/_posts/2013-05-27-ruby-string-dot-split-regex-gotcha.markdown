---
layout: post
title: "Ruby String.split Regex Gotcha"
date: 2013-05-27 09:38
comments: true
categories: ruby basics gotcha
---

### Using String.split and a regexp input might not behave how you think it should. 

Yesterday I was a attempting to split an input string into an array of nine character wide strings.  String.split seemed like a perfect tool for the job. However, I found a slight problem. Any regular expression sent to split is treated as the delimiter, not the capture.  This results in the empty array as there is nothing in between the splits to collect into the array.

```
"1234567890111222333444555666".split /\d{9}/
=> []
```

We can verify this by adding a delimiter to the input string.

```
"123456789,111222333,444555666".split /\d{9}/
=> ["", ",", ","]
```

The "aha" moment is the regular expression is used to determine the delimiter, not the captured values.  This is a bit different than I expected.  So being clever, I thought, let' use capture groups in the regexp.

```
"1234567890111222333444555666".split /(\d{9})/
=> ["", "123456789", "", "111222333", "", "444555666"]
```

Wait, what happened?  Why the empty strings still?  Remember, it is still using the regexp for the delimiter. The text that is not part of the delimiter is still returned.  The captured text from the regexp is also returned.

It is stated in the ruby core docs, it just isn't so clear what is going on until you test it like above.

> If pattern is a Regexp, str is divided where the pattern matches. Whenever the pattern matches a zero-length string, str is split into individual characters. If pattern contains groups, the respective matches will be returned in the array as well.

So what is the correct way to accomplish our goal of splitting the text into 9 character length arrays when no delimiter is present?

####String.scan

```
"123456789111222333444555666".scan /\d{9}/
=> ["123456789", "111222333", "444555666"]
```

So lesson learned, always check your assumptions.  Thankfully, unit tests showed me what I was doing wrong before this got really ugly and hard to chase down.

