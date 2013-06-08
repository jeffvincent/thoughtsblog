---
layout: post
title: "Jekyll YAML Test"
description:
  If you are using Jekyll, broken YAML can ruin your build (and day). Here's a
  quick test you can add to your suite to make sure you didn't inadvertently
  break anything.
category: Rspec, Jekyll
---

My goal with the [Wistia Doc](http://wistia.com/doc/) was that everyone on the
team could contribute. Part of making that a reality is making sure all sorts
of edge cases and potential problems are covered - I don't want everyone to
have to know the inner workings of Jekyll in order to contribute.

The YAML metadata block in Jekyll makes it super easy to use, but YAML is also
not widely used among our team and can be fairly brittle. Jekyll doesn't do a
great job reporting issues if a YAML error breaks the build - someone could
push an update and continue on their day happily, not knowing they just
completely broke new content generation.

I added a simple YAML test into our build rake task and Rspec tests to test the
YAML for each post. Maybe it will be useful for you too!

Here is the Rspec test I wrote - doesn't do much except check the YAML block.
It should let you know if there was an error in your YAML and if so, which post
it was in (which Jekyll won't tell you {{ ":wink:" | emojify }}).

At some point I'd like to figure out how to test all links too, to make sure
they point to real content. Moving doc pages and 404s are the bane of my
existence!

{% codeblock jekyll_yaml_test.rb %}
require_relative 'spec_helper'

describe "Content" do

  before(:each) do
    @posts = []
    Dir.foreach('_posts') do |p|
      @posts << IO.read("_posts/#{p}") if p.match(/^[^.]\w/)
    end
  end

  it "should have valid yaml" do
    @posts.each do |post|
      begin
        YAML.load(post)
      rescue Psych::SyntaxError => e
        pp e
        pp post
        raise "Post syntax is not valid"
      end
    end
  end
end
{% endcodeblock %}

One thing I should mention - the regex test for adding a post is pretty 
simple - it's just meant to keep the `.DS_Store` file out. We don't use dates
in our doc posts - but you might (and I do in my blog).  If so, you might want
to test and make sure the post title starts with dates separated by dashes!

Thanks to [Robby](http://twitter.com/freerobby) for the help!
