---
layout: post
title: "My Octopress Setup in the Cloud"
date: 2013-01-08 06:00
comments: true
external-url: 
categories: Site
author: Dan Robbins
published: true
---

#### *Or, How a non-hacker set-up a "blogging framework for hackers"*

In starting this site, I had a few objectives besides posting about the markets. I got my first internet account in 1995, and it came with a whopping one megabyte of "personal web space." I thought about what to do with that, as I wanted to learn how to make a web page but didn't know what to put on it. My roommate at the time, suggested, "How about your margarita recipe?" Bingo, that was it. I learned how to code html and put up my website, titled, "Spike's World Famous Margaritas" and to borrow the term, I built it and people came, mostly through the Yahoo directory of the time, and by people sharing links. I had a guestbook on the site, coded in Perl and would get several entries a week, which was awesome. The url was ugly, like http://www.deltanet.com/~users/spike/margarita.htm as it was provided by the internet provider. 5 years later in 2000, I finally made a permanent home for my site at [blenderking.com](http://www.blenderking.com). The switchover was part of a project to teach myself Cold Fusion, and I loved what I learned about creating a database driven website, but that will be another post. I later switched to Wordpress after kids sucked up my coding time.

For this new website, my objectives were:

* Learn more about cloud computing, using Amazon Web Services and EC2 as a reference point
* Learn more about the command line and working with [Git](http://git-scm.com)
* I wanted another avenue for writing
* Get back into learning programming, modifying code, as well as learn [Markdown](http://www.daringfireball.net/projects/markdown)
* Create a separate website for market oriented postings

Overall, I found [Octopress](http://www.octopress.org) to be exactly what I wanted. I first encountered via [Matt Gemmell's site](http://mattgemmell.com). The default design is great, and as I learned more, I was intrigued by the prospect of creating my own site based on it.

#### Why I went with Amazon EC2, with a dash of Dropbox mixed in

<!-- more -->

Interestingly, I've found it to be common for most of the people running Octopress to write a post how their individual setup and configuration. Most generate the site on a Mac, then push the html pages to a webhost. After struggling a bit with setting up SSH and Git properly on my Mac, I decided this was the opportunity to use Amazon EC2 as a learning opportunity. I'm glad I did! But it came with a learning curve to do it the way I wanted to. Here's my general process for writing a post:

* Type the post on my Mac using TextMate
* Save it to specific folder inside of [Dropbox](http://db.tt/aTciVolG)
* Go to the AWS console, start up my micro EC2 instance
* Once the instance is running, generate the site and copy it to the Apache htdocs folder for testing on the server
* Edit, re-generate, and test if neccessary
* Deploy the site to my host, in this case, I'm using [Github pages](http://pages.github.com) but I'm also set up to deploy to Amazon S3. It's just a configuration and DNS change to switch.
* Turn off the EC2 instance. If I'm within 1 hour, I spent 2 cents to generate and deploy the site.

Yes, 2 cents an hour. That's how much I pay to rent a Linux server via Amazon. In my mind, that's utterly amazing. Quick math - if I write 10 posts a month, that's 20 cents a month to rent the server. (Plus monthly EBS volume changes, which for my use is about a dollar/month). In time, I might find that generating the site takes longer. If I wanted to, I'd have the option to migrate to a larger instance. For example, a Medium High CPU instance is 16.5 cents an hour. The same 10 posts a month would cost $1.65. [Here's the EC2 pricing](http://aws.amazon.com/ec2/pricing/). Amazing.

#### Major Advantage - this seemingly convoluted setup is iPad friendly!

I structured it this way so I could create posts from my iPad (and an iPhone too if I really wanted to). All the ingredients are there:

* I can turn on and off the EC2 instance via Amazon's web based console
* [Dropbox](http://db.tt/aTciVolG) is installed on the EC2 instance with it symlinked to my octopress/source/_posts folder
* I create/edit posts on the iPad using [Nebulous Notes](http://nebulousapps.net)
* I connect to the EC2 command line, for generating and deploying the site via [Prompt](http://panic.com/prompt/)
* Keep in mind the IP address of the EC2 instance changes with every restart. You could, optionally, create an elastic IP address in AWS, which costs 1/2 cent per hour when the instance is not running
* I set up aliases in my EC2 bash profile to save keystrokes. Prompt also provides auto-completion of prior used commands.

Furthermore, Nebulous Notes has macro ability; I was able to create a template of the YAML front matter for the Octopress post, saving on typing when creating a post on the iPad. The [Dropbox](http://db.tt/aTciVolG) setup works perfectly - I can create a post on my Mac and continue editing it on my iPad, and vice-versa (as I did in creating this lengthy post) Furthermore, I also have a folder for images that is symlinked between Dropbox and Octopress too. 

#### How I got the site up and running:

* I Used [Bitnami Rubystack](http://bitnami.org/stack/rubystack) - this made things so easy. A few clicks and I had all the software installed in my EC2 instance. Ruby, GIT, Apache, etc. No muss, no fuss
* Installed Octopress from Git, from my own fork. (note - had to sudo some commands, i.e. bundler)
* Setup ssh to [Github](https://help.github.com/articles/generating-ssh-keys#platform-linux)
* Setup [s3cmd](http://s3tools.org/s3cmd) for command line access to Amazon S3. This [site was helpful](http://www.jerome-bernard.com/blog/2011/08/20/quick-tip-for-easily-deploying-octopress-blog-on-amazon-s3/). Note, I found it worked better to paste the keys in, not type them in.
* Setup [Dropbox](http://db.tt/aTciVolG). This [site's](http://buildcontext.com/blog/2012/dropbox-linux-ubuntu-ec2-linode-selective-sync) instructions made things easy.
* Configured the site to my needs; the [Octopress docs](http://octopress.org/docs/theme/) cover a lot, or do some searching. I also found it helpful to search Twitter for any mention of Octopress.
* Oh, and actually write some posts, that's the whole point, right?

#### Final Thoughts

I really enjoyed setting the site up. I learned what I set out to learn and am very pleased with how the site looks. Also, with my setup, it's super cheap to run. Sure, it would be free if I used my mac and github but my expense is minimal. I'm thankful for the community around Octopress - I learned from so many people who had posted their setups. I'm still learning about VIM and the command line but feel much more comfortable already. I think I'd like to set up my own theme as a way of re-learning CSS and design.

*Ultimately, the site is about the content*, and I'm using this site as a platform to post charts and my general thoughts on the markets. So I've combined two hobbies into one!

