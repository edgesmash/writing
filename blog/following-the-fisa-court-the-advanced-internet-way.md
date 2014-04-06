<a href="http://sudden2.deviantart.com/art/Floyd-s-Prism-51863247" target="_blank"><img src="/assets/images/prism-wide.jpg" style="text-align: center" /></a>

A couple weeks ago, I created [@FISACourt](https://twitter.com/fisacourt), a Twitter account that automatically posts whenever the [Foreign Intelligence Surveillance Court website](http://www.uscourts.gov/uscourts/courts/fisc/index.html) is updated. I created it in about 5 minutes, using ChangeDetection.com and IFTTT, and [blogged about how it](/post/following-the-fisa-court-the-internet-way) works. 

After I did that and @FISACourt got a few followers, I realized this would not be good enough. In my experience, [IFTTT](http://ifttt.com/) checks RSS feeds once an hour, and ChangeDetection's [FAQ](https://www.changedetection.com/faq.html) says they check pages just once a day. That's potentially a 25 hour delay — not so good for breaking news.

So I wrote some code to check the FISA Court myself, and set it to run every 5 minutes, using my web server (the same machine that serves this blog). You can find the code at [github.com/konklone/fisa](https://github.com/konklone/fisa), along with instructions for setting it up yourself.

This new setup does more than check for changes and update a Twitter account — it also sends me an email and a text message so that I know an update just went out. This way, I can quickly figure out what changed and promptly add some human explanation of what the FISA Court just did, like so:

<blockquote class="twitter-tweet"><p>FISA Court just ordered the US to redact and declassify its 2008 opinion ruling against Yahoo, and associated briefs: <a href="http://t.co/wF547a8iCZ">http://t.co/wF547a8iCZ</a></p>&mdash; FISA Court (@FISACourt) <a href="https://twitter.com/FISACourt/statuses/356878749649739776">July 15, 2013</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

It's written in Ruby, and optionally uses [Twilio](http://www.twilio.com/) for text messages (which cost me all of one penny apiece). For emails, you need to use an SMTP server (you can [use your Gmail account](http://email.about.com/od/accessinggmail/f/Gmail_SMTP_Settings.htm), but Google doesn't like to talk about it), and to connect it to Twitter, go to [their developer portal](https://dev.twitter.com/) and create an application for the account you want to post from. 

The initial version was only [82 lines](https://github.com/konklone/fisa/blob/caf710dcc61a17ab335648095fa52a86ecf7aadd/fisa.rb), and would just download the Court's site and compare files on disk to see if they were different. It worked, and it was fast, but it was also clumsy: if you (as a follower of @FISACourt) wanted to know what changed, you had to either wait for me to hop on and explain, or dig around the site yourself until you find the new things. I kept records of the changes, but only as files on my server, and the first time the FISA Court updated, I [mistakenly](https://twitter.com/FISACourt/status/351769853226516480) thought it was a trivial change because I misread the changes. Amateur!

So today, I published and documented my code, and [announced](https://twitter.com/konklone/status/353960261398433793) my intent to automatically show diffs using GitHub. [Ben Balter](https://twitter.com/benbalter) immediately jumped on it and [added that GitHub integration](https://github.com/konklone/fisa/pull/1) in an hour. I shored it up a little further, and from now on each automatic tweet from @FISACourt will also include a link to a nicely rendered view of the changes (like the example above).

The whole thing is still very simple, [just over 100 lines](https://github.com/konklone/fisa/blob/cc5665bf7ba5fb75be4da7dfa233fbb94e15c7fb/fisa.rb), and easy to set up. It's a little bit of glue that pulls together powerful services that cost little to no money, and needs no one's permission.  **Internet.**