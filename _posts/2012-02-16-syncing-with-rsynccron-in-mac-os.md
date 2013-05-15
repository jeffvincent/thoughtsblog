---
layout: post
title: Syncing with Rsync/Cron in Mac OS
tags:
- jobstuff
status: publish
type: post
published: true
meta:
  jabber_published: '1329404434'
---

**nerd alert!** This post chronicles a super SUPER nerdy undertaking of mine.  
I'm going to try doing this more often, in the vein of putting out resources I 
wish I had found when embarking on such a project.

Dropbox is *awesome*.  I use it for lots of personal stuff, and we use it at 
Wistia for work stuff as well.  I'm also big into Time Machine - I have a 2.5TB 
Time Capsule at my apartment that backs up my laptop and Marisa's laptop every 
night.  

So my data is pretty safe.  But I've always been missing a way to actually MOVE 
files from my work laptop (Macbook Air with 125GB SSD) to my home Mac Mini 
(connected by ethernet & USB to the Time Capsule) without having to manually 
connect and drag it over.

I've been pretty obsessed with keeping the Macbook Air clean, so I started a 
directory on my Desktop called `For Other Books`.  I would drag PDFs, music, 
and video for backing up here, and then next time I thought of it, I would 
transfer that to it's proper place on the Mac Mini/TC setup.

This worked pretty well for a while, but I wasn't using it much because it was 
cumbersome and annoying.  I tried moving that directory into Dropbox, but that 
slowed the network to a halt (as it uploaded the 1+ GB original
[Wistia team video](http://wistia.com/about/company)).  

It also required an extra step, since I then had to boot up the Mac Mini and 
move the file from the Dropbox directory to the Desktop.  Still not awesome.

I did some looking around the web and came across [this article on Lifehacker](http://lifehacker.com/196122/geek-to-live--mirror-files-across-systems-with-rsync)
about using [rsyn](http://everythinglinux.org/rsync/), a command line utility 
for syncing.  Some time and plenty of interesting issues later, I now have a 
much better set-up: every Sunday at 2am, a directory on my Desktop is synced 
with a directory on the Mac Mini.  It then deletes the files within the 
directory on the Macbook.  What follows are the steps I used to achieve this.

"But what about tool XYZ?" you ask.  Well I didn't try that tool, so get off my 
back {{ ":grimacing:" | emojify }}.  Instead I looked for the most automated and
open-source option I could find, mostly so I could learn how the whole thing 
worked.  

It took me approximately 3 hours to get this all working -- most of it spent 
scouring the Internets each time I encountered a problem.  That's why I'm 
writing this post: so someone with similar inclinations and ambitions will be 
able to do the same thing without (as much) trouble.

## The Setup

* Macbook Air, OS X 10.7.x
* Mac Mini, 10.7.x
* Time Capsule

## Step 1: Setting up SSH

The first step is setting up SSH between your local computer (MB Air) and the 
remote machine (Mac Mini).  To accomplish this even when the Macbook Air is 
remote, we need to set up port forwarding on the Time Capsule.  So I Screen 
Share into the Mac Mini and pop open Network System Preferences and the Airport 
Utility.  

Right about **now** is when I discovered that the latest version of the Airport 
Utility deprecated advanced options (what the???).

Luckily, our boys at MacUpdate have maintained a link to the [old version](http://www.macupdate.com/app/mac/19858/airport-utility).
Downloaded version 5.6.  Ahhh, advancedy goodness.  

Pop open the `settings -> Internet -> NAT`, and make sure the 
`Enable NAT Port Mapping Protocol` checkbox is checked.  Click the `Configure Port Mappings...` 
button, and add a new device to the list.  

You can leave the "service" drop-down blank, set all the ports to `22`, and in 
the Private IP Address, I added the IP address for the Mac Mini (which you can 
grab from the Network System Preferences).  So now, to SSH into my Mac Mini, I 
can use the IP address of my Time Capsule (which you can see in the TCP/IP 
panel of the Airport Utility).

<div class="post_image"><img src="http://embed.wistia.com/deliveries/387e06202ea4f5d5b3dbb360dac35a7472d0638e.png" alt="shot1"></div>
<div class="post_image"><img src="http://embed.wistia.com/deliveries/62a46f7bfc2e5a65cc374f27c35a730ee0d91210.png" alt="shot2"></div>

With that mess complete, I could now SSH into my Mac Mini from the office using 
a command like the one below (replacing the X's with your Time Capsule IP address):

{% codeblock term1.sh %}
ssh jvmini@XXX.XX.X.X
{% endcodeblock %}

I could now complete a successful rsync sync for the first time as well 
(command is all one line):

{% codeblock term2.sh %}
rsync -avz --progress /Users/jv/Desktop/forotherbooks/ jvmini@XXX.XX.X.X:/Users/jmini/Desktop/fromotherbooks
{% endcodeblock %}

## Step 2: Public Key Authentication
Hooray!  Since I knew I wanted to end up being able to do this automatically, 
entering the password each time wasn't going to be an option.  We use public 
key authentication for a few things in the office, so I had an idea of getting 
that set up, but if you are new to that game, check out [this guide](http://macnugget.org/projects/publickeys/).  

Here's the run-down of the commands used:</p>

{% codeblock term3.sh %}
ssh-keygen -t dsa
scp ~/.ssh/id_dsa.pub jvmini@XXX.XX.X.X:.ssh/authorized_keys
ssh jvmini
{% endcodeblock %}

## Step 3: Enter the Cron

Now I had sync set up and working, but the automated part was still missing.  
For that, I needed cron.  [Cron](http://en.wikipedia.org/wiki/Cron) is a UNIX 
tool for scheduling jobs - pretty cool if you want to automate stuff and have 
it run on schedule.  I didn't have any experience with cron at all, so it took 
me a little while to get a handle on it.  

Basically, there are two parts: the **script** and the **cron table**.

The script I wrote wasn't too complicated - essentially sync everything up, and 
the delete all the old files from the local directory.:

{% codeblock term5.sh %}
#!/bin/bash #This says which interpreter you want to run the script under (in this case bash)

RSYNC=/usr/bin/rsync  # this tells the interpreter where to find rsync (run 'which rsync' to be sure)
SSH=ssh   # find SSH in the same place as rsync
LPATH=/Users/jeff/Desktop/otherbooks/   # read: "where is the local computer path you wish to sync?"
RPATH=jeffmini:/Users/jeffmini/Desktop/fromotherbooks   # read: "And what about the remote path?"

echo "Syncing and it feels so good" # I put this mostly for myself.
   
$RSYNC -avz --progress $LPATH $RPATH >> /tmp/output.txt   # this is the rsync command, and then '>>' tells the interp to put the output into a text file (like a log)
cd $LPATH   # CD into the local path
rm *    # delete all the files that are left in there after the sync
{% endcodeblock %}

I saved this under the title *sync_books.sh* and saved it for now in my Home 
directory.

Next was setting up the cron table.  Cron table is a config file where your list 
of jobs are for executing.  This step was a bit tricky, since the normal command

{% codeblock term6.sh %}
crontab -e
{% endcodeblock %}

Wasn't working properly for whatever reason.  I blame Apple but that's ok.  
I found a workaround, which is to use the editor [Nano](http://www.gentoo.org/doc/en/nano-basics-guide.xml),
rather than VIM, to edit the crontab file.  In retrospect, this makes sense, 
since Apple has been tried deprecating the use of cron in favor of something 
called launchd.  Anyway, here's the command for opening the crontable in Nano:  

{% codeblock term7.sh %}
EDITOR=nano crontab -e
{% endcodeblock %}

This opened up the cron table, so I could add a new line to it.  Cron tables 
(or at least my limited understanding of them) have syntax like so:

{% codeblock term8.sh %}
* * * * * command to be executed
{% endcodeblock %}

The asterisks in this case stand for min (0-59), hour (0-23), day (1-31), 
month (1-12), day of week (0-7, 0 and 7 are Sunday).  

A great tutorial for Cron table syntax is over at [Admins Choice](http://adminschoice.com/crontab-quick-reference) 

## Step 4: Testing

Since I was setting up the cron job to run once a week (2am Sundays), I didn't 
want to wait that long to make sure it worked.  A one-line addition to my cron 
table file ran the cron script immediately:

{% codeblock term8.sh %}
*/1 * * * * /Users/jv/sync_books.sh
{% endcodeblock %}

And then running a tail command in the terminal, to track updates to that 
`output.txt` file:

{% codeblock term8.sh %}
tail -f output.txt
{% endcodeblock %}

And a minute later, voila! Syncing was complete!  Now I can dump all the stuff 
I want to access on the Mac Mini (or archive) without clogging the network, or 
dumping it into the Time Machine abyss.  Enjoy, and let me know if you have any 
questions!
