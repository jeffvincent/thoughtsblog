---
layout: post
title: "On Status Page Design"
description:
  We recently released our new Wistia status page, codenamed Bugle. Here are
  some of lessons learned from the design process.
category: startups, design
---

We had a [recent infrastructure issue](http://wistia.com/blog/playing-reveille-creating-the-wistia-status-page/)
that knocked out one of our key features for nearly a week.

This was a big deal to us, and a big deal to our customers as well. As we were working
on the technical side of it, to fix the immediate issue and shore up our
infrastructure for the future, we also worked on the support side of the problem.
We wanted to improve our communication processes for major outages like this one.

The major project that came out of this work was [Bugle](http://status.wistia.com),
our Wistia status page. We had always been keen on the idea of creating a
status page, but had trouble elevating it to the priority it deserved. This
issue gave me the kick in the pants needed to get to work on it.

I can't make something look good to save my life, but luckily I work with some really 
talented designers. I snagged Liat to help me mock-up the layout, and I think 
it ended up with a design that fits our requirements *and* looks good.

For folks that might look into building their own status pages, here are some
of the lessons I took away from the design process.

<div class="post_image"><img src="http://embed.wistia.com/deliveries/2fea5e1c06935c714ecc75a9f80ce6cf5700bb0b.png" alt="bugle homepage"/></div>

## Yes, the Design Really is Important

Before we jumped in, we needed to answer the overriding question: "Was our status 
page design is even important?" The prevailing advice on status pages seems to 
be "just get something up there".  Before we began work on our design, I looked
at the status pages of some of the most popular services. Many were just plain
data dumps - ugly and confusing.

Our customers love us because we keep things simple, organized, and sane. They
trust us to communicate what is important, and keep the noise to a minimum. Our
status page needed to look more refined.

## Yes, the Status Page is Part of Your Product

The true measure of a service is when the carefully architected workflow breaks 
down, and the customer needs help. They were humming along, loving your
product, and suddenly something goes wrong.

They track down your status page, and when it loads it looks completely alien to
them. It has an old, crusty logo in the corner, the color scheme offends the 
senses, and the fonts carefully selected for your marketing site are swapped
for Comic Sans.

It's like that scene in *Terminator Salvation* when the dude realizes he's
really a cyborg. Your customer was just torn from app bliss, and realized your
product is just a machine after all. *[Noooooo!](http://nooooooooooooooo.com/)*
That's bad! Even when the shit hits the fan, we want to keep the technology 
hidden in the background. Why?  Because our customer's pay us for video hosting 
and tracking, not for the technical mechanics behind those things!

While it isn't the most positive part, the status page is still included in your
customer's total experience, and needs to feel that way. Your status page should
have the same look and feel as the rest of your product.

## Know Your Customer

It all starts with the customer. In particular, make sure you are clear on what
their state-of-mind people will be when they land on your status page. Here's a
hint: they will be confused, concerned, and stressed. 

The last thing we want to do is add to our customer's daily stress!

So given an app issue (the thing that makes the status page necessary), what
information will your customer need? What questions are they likely to want to
ask? Your design will need to answer these questions, and also bring them back
to their normal, productive state.

Our main questions:

* is a part of Wistia down?
* if so, who does it affect?
* when is it likely to be fixed?

Based on who uses your product, it's also important to know which "profiles" of
user will be viewing your status page. Our main groups:

**Marketers**: Many of our customers are marketers. They want to know if a major
part of the infrastructure is down, and if so, how they are affected.

**Business Ops**: There are a number of businesses that rely on Wistia to deliver
the bulk of their product's value. 

**Tech Teams**: Be they the IT team for a large company, or a technically-inclined
customer (which we have lots of as well, it's awesome!).

## Priority is Key

Each of our interest groups (listed above) would have a different level of
investment in the information a status page could provide. Some would want a
quick infrastructure overview, others would be interested in the nitty-gritty
of the technical issue we were experiencing (and how we ended up solving it!).

**At a Glance View**

For the high-level overview, a simple <i class="icon-check-sign" style="color: green;"></i> or a
<i class="icon-remove-sign" style="color: red;"></i> alone weren't going to cut 
it. We expect more from ourselves, and our customers do too. 

<div class="post_image"><img src="http://embed.wistia.com/deliveries/d0115fe9a26106f9e5ab7151954578771e44336e.png" alt="services status icons" /></div>

Joe and Liat teamed up to create a set of icons, one for each Wistia service.
These provide at-a-glance status, *red*, *yellow*, or *green* (hopefully they
are green all the time).

**In-Depth Posts**

Especially when things are down, we needed a place to explain the issue and a
timetable for when a fix would be ready. To make this status page a customer 
support win, we needed to be able to speak to customers the same way we'd
been talking to them via email and phone calls for years - clearly, calmly, and
respectful of their time. The awesome part was, we could now do this at scale.

<div class="post_image"><img src="http://embed.wistia.com/deliveries/362c878bbd5399dbec7f43424ffb1a461ffb517d.png" alt="service alert example" /></div>

Our alert posts were also designed to be perused or delved into. Each one shows
the date of the alert, the title (hopefully crafted to be useful and clear),
and a *status dot*. That makes it easy to identify what service is affected and
what the most recent status is.

On page load, only the most recent status alert is 'open', while the rest are
'closed' (title, date, and status would show only). Anxious visitors
experiencing an outage can concentrate on our latest update, instead of being 
distracted by other content. Long-term, we're also being transparent about what 
happened - the *red*, "status down" post doesn't disappear immediately once the
service goes to *green*.

## Keep it Clean

Our original plan was to use a blogging service, like Tumblr, to house our
status page. It would make it easy for anyone on the team to post a status update.

The problem was *clutter*. After a reasonable amount of time, people wouldn't care 
about our old status updates, and they might take them out of context as
commentary on our abilities. In the end, we rolled our own Rails app to solve
this issue.

To further drive down the amount of text on the page, and to keep updates from
being buried, we stole the idea of excerpts from Medium. This prevents longer 
posts like post-mortems from clogging up the entire status page.  

Each alert has a permalink, to make it easy to share a Wistia status with
your team, and so we can put the full text of a longer post somewhere.

---

When something goes *bump* in the night for our customers (especially if
it really does happen overnight, when our Customer Champions are getting their
much-needed sleep), our status page should give them the info they need to make
informed decisions and feel more confident using our services.

My advice: make building a status page a priority, and get the resources to do
it right. Put the same care into it you put into your other customer-facing
resources, like your blog, your documentation, and your website. When it is
actually needed, it will be well worth the effort.
