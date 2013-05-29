---
layout: post
title: Playing Reveille - On Creating The Wistia Status Page
description: After a recent outage of our stats infrastructure, we knew we
  needed to have a place to let our customers know what was going on. This is
  the story of how Bugle was born.
category: startups, product, support
---

"Integerocalypse" is a word that has been spoken in hushed tones around the
office for a long time. While I'll let [Ben explain it in better technical detail](),
here's the gist: *all analytics data for all our customers is held in a
database. When that database passed 2.2 billion records, all hell was set to break
loose.*

While we took strides to avoid the issue, we couldn't quite escape it's
clutches. When we passed that mythical number, stats had to be taken offline, 
and they ended up running behind for nearly a week. This was terrible news for
our customers, many of whom depend on our analytics for making daily business
decisions.

This issue forced us to think a lot more critically about how we communicate
issues to our customers, and how can improve them in the future.

Here are some of the lessons we learned:

## Have a process in place ... before an issue occurs

We get scared of putting process in place - it sounds like something for big 
corporations, not us. But a lack of process can cause confusion and lead to 
critical pieces getting dropped on the floor. You don't need to be completely 
prescriptive, but get the basics down.

And it's not just *what* needs to be done, it's also by *whom*. It's a great 
first step to have a skeleton process in place, but you are not completely out 
of the woods. Just as in important is to assign clear roles, so that folks know 
exactly what action they are expected to take. This further reduces confusion 
and enables quick action.

## Categorize, then Attack

Not all outages are created equal. For us, we have two key buckets: **internal
issues** (*those that only affect our direct customers*) and **external issues**
(*those that affect our customer's customer as well*).

Once you determine who is being affected, it is much easier to determine the type 
of communication that is appropriate.

In the example of our stats running behind, our direct customers were affected,
and the issue would manifest itself on the stats pages in their account. This 
meant communicating the outage should happen in-app (where our customers could 
see it) and on the stats pages specifically (where it was most relevant).

## Communicate thoroughly, and keep those affected up-to-date

In-app messages are great, because they can be pointed and timely, but you may 
not have room to communicate everything you need. Twitter is the same way - 
140 characters is just enough room to incite panic, not to actually communicate 
the real issue.

We needed a good place to point interested/affected customers, where they could
read up on the issue and get a good sense of where in the process we were.

I'll admit, we're pretty behind the times, but it was time to build a [status page](http://status.wistia.com). 
Codenamed `Bugle`, after the simplest brass instrument, it is designed to 
communicate quickly and clearly what issues our infrastructure might be 
experiencing, and keep customers in the loop.

<div class="post_image"><img src="http://embed.wistia.com/deliveries/fe5aee6f0c8535b8d7c6512efc82b3fe35110bc3.png" alt="Bugle version 1" /></div>

It provides us a place to point to when we quickly communicate issues in-app or
through Twitter. From a support perspective, it also helps resolve the
long-term problem of local issues (read: Flash plugin problems) presenting like 
app-wide problems. Bugle gives concerned customers a place to check to see 
"is Wistia experiencing issues?".

## Fix it Twice

Joel Spolsky wrote a great post, [Seven Steps to Remarkable Customer
Service](http://www.joelonsoftware.com/articles/customerservice.html) that gave
me a roadmap to tackle my Wistia position and that I turn to for inspiration often.
I'd go and give it a read, if you haven't already.

I'd argue we've been following this advice for a long time, but on an
individual basis. We've been fixing the root issue, and following up with
customers who reached out via email. It's time we made this communication more
transparent.

The [first post]() on Wistia Status is a postmortem of *Integerocalypse*. I
hope you'll give it a read. It's a great write-up of what went down and what
we're working on to prevent it from happening again.
