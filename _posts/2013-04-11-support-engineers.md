---
layout: post
title: Support Engineers
description:
  A further discussion of using in-house engineers to help solve
  technical support issues.
category: support
---

A few weeks ago, Chase Clemons invited me to join him on Support Ops, his
weekly podcast. It was a ton of fun - Chase is very well versed on the topic,
so we could talk openly about challenges we faced and how we were overcoming
them in our own practice. The recording (which you should totally check out) is
over on the [Support Ops site](http://supportops.co/the-customer-champion-with-jeff-vincent/).

Before the show, [Alyssa](http://twitter.com/alyssaaldersley), one of the
awesome Happiness Heroes at Buffer, requested we talk about support engineers,
and their role in providing support. We covered it as one of the show segments, 
but I don't think I really did the question justice.

The crux of the question is something I'm sure all support folks have pondered:
*how to escalate the tough technical questions without distracting the folks
who are building new features into the product*.

From my limited experience, a lot of other companies approach this by having a
designated "support engineer", someone who has a background as an engineer, but
devotes much of their time working on support issues. Chase and
[37signals](http://37signals.com) have rotating "support engineer" time. This
functions very similar to an *all hands support* model, in that everyone
participates in the support process, but in most instances I've heard of, the
support engineer doesn't actually communicate with the customer. They just
answer the technical question. Definitely good in some instances, but we
weren't sure about ours.

A few months ago our support team (myself, Max, and Jordan) got together and
thought through the question. It sure was annoying to have to bug each other 
and our dev team to get answers on certain issues - and it also wasn't a 
good experience for the customer. The toughest questions just kept piling up in
the bottom of the inbox, since we didn't have the bandwidth or knowledge to 
answer them.

We decided the only way to get customers the highest quality support possible
was for the support team, and future folks that want
to [join us](http://wistia.theresumator.com/apply/5Ozymq/Customer-Champion.html),
to act as our own support engineers.

There were three big motivating factors:

  1. We hate bugging people to help us (and we stink at getting them to do
     stuff for us).
  2. We want to get customers the help they need, super fast.
  3. We are interested in learning new technical skills, and contributing to
     the growth of our product.

Just to clarify before I continue, this doesn't mean we became engineers
overnight. There are still plenty of times we have to bug the developer that
built the feature about. But our goal over the long-term is *decreasing* the
volume of requests that need to go through our dev team, while simultaneously
*increasing* the quality and speed of our responses to customers.

There are ups and downs on both sides of this argument. If you are currently in
this situation, here are a few reasons to go what I'll call the *Customer
Champion route*.

### Faster Learnings, Better Shared

Having a dedicated support engineer would probably mean fewer total headaches -
the number of issues we spend time investigating that a trained engineer would
be able to quickly or effortlessly handle is significant. We still have lots to 
learn which means it's slow going at first.

That being said, we've done a great job sharing our learnings and improving as
a group - which I think has helped our communication processes. The dev team
also really appreciates that we handle more of these problems ourselves!

If you can, put together a shared document that support folks can contribute to
as they learn new things. Our *Moreau Doctrine* contains the basic outlines of
some of the toughest/most counterintuitive questions, a bunch of
troubleshooting tips, and even Rails console commands worth remembering. This
means no one has to struggle through the same thing twice, and new people added
to the team have a great starting place so they can catch up quick.

### Cumulative Learnings Lead to Exponential Growth

One of the *worst* parts of a support person's day, in my opinion, is when an
issue comes in that sits right on the border between doable and not doable.
Like it's technically possible, but would require bugging an engineer to write
a custom report or would require some API work. The types of things we'd want
to build into the product in the long-term, but aren't working on today.

In those instances, the response the customer gets is affected by how long the
queue is, how busy the team is, and how caffeinated the support person is,
among other things. That's not great support.

As we've developed our skills, the support team has actually been able to
tackle these projects ourselves. Our [demobin](http://wistia.github.com/demobin)
contains little API projects customers can now use on their own sites. We have
internal scripts to generate in-depth stats reports, an issue that had been
dogging us for a long time. The people who face the problem every day should be
given the tools to solve it, if they so choose.

### Support is About More Than Technical Issues

We've had it on the list to get our *all hands support* mode rocking again for
some time. For a while there, the dev team was on call for lots of issues, so
it felt like all hands support anyway. But as we've progressed, developers are
forced to deal with fewer technical issues, and can get their hands dirty
answering the normal customer requests again.

This will pay enormous dividends into the future. Having a real connection with
our customers helps in pretty much any decision we make, and I credit the
success of Wistia to having our customers interests at heart.

---

If your support team has the interest and the drive to make it happen, I
suggest going to Customer Champion route. Let me know how it goes!
