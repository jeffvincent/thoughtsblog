---
layout: post
title: "Using Sass Hashes"
description: 
  Sass has powerful hash functionality that you can use to further simplify your style.
  This quick example will get you started.
category: development
tags: development, sass
---

When Robby and I were working on the [Wistia Status Page](http://status.wistia.com),
I ran into what I consider a pretty common problem - a consistent group of
subclasses that just cluttered up the stylesheet. In this case, the subclasses reflected
the different status settings - *down*, *degraded*, and *up*.

The original code looked something like this:

{% codeblock original-code.sass %}
.app-icon
  margin: 0 auto
  width: auto
  height: auto
  line-height: 100%
  font-size: 45px

  &.red
    color: $red-status
  &.yellow
    color: $yellow-status
  &.green
    color: $green-status
{% endcodeblock %}

Not so bad, right (if you can excuse my variable naming)? But this sort of
pattern happened 3-4 times around the codebase, so I was somewhat motivated to
clean it on up.

My first instinct was to use a `mixin` for this. Here's what my attempt at the
mixin would look like:

{% codeblock statusii-mixin.sass %}
=status-settings
  &.red
    color: $red-status
  &.yellow
    color: $yellow-status
  &.green
    color: $green-status
{% endcodeblock %}

Pretty straightforward, also doesn't do anything. I just moved the code from
one place to another. When I went to style the `Flash` messages, which came in
*error*, *notice*, and *info*, I was right back where I started.

I was looking for a way to handle both, since they used such similar styles.
That was when I came across [Nathan Henderson's](http://twitter.com/nathos)
post on [Sass Hashes](https://gist.github.com/nathos/1212291).

Cool, I thought, I'll give it a try! Here's what the final code looks like:

{% codeblock final-code.sass %}
// variables area
$status-settings: "red" $red-status "error", "yellow" $yellow-status "notice", "green" $green-status "info"

// style area
.app-icon
  margin: 0 auto
  width: auto
  height: auto
  line-height: 100%
  font-size: 45px

  @each $status in $status-settings
    &.#{nth($status, 1)}
      color: #{nth($status, 2)}

.flash
  @extend %content-box
  display: none
  padding: 20px
  font-size: 16px

  &.info, &.error, &.notice
    color: white
    font-weight: 300
    letter-spacing: 1px

  @each $status in $status-settings
    &.#{nth($status, 3)}
      background-color: #{nth($status, 2)}
{% endcodeblock %}

So what the heck is this doing? Super quick breakdown of the `@each` statement:

{% codeblock each-statement.sass %}
@each $status in $status-settings
  &.#{nth($status, 1)}
    color: #{nth($status, 2)}
{% endcodeblock %}

The first line `@each` interates over each comma-delimited group in the
`$status-settings` hash. So the block is working on, for example, the group of:

<code class="fullwidth">"red" $red-status "error"</code>

Inside the block, the `nth()` method takes two arguments: first the object the
block is working on, and second the element in the list (note: 1-based indexing,
so it starts at 1 and not 0).

The `#{}` around the method mean it will be interpolated. So when the argument

{% codeblock sample-argument.sass %}
&.#{nth($status, 1)}
{% endcodeblock %}

returns `"red"`, this will be interpolated in-place to read: `&.red`.

Pretty neat, huh?
