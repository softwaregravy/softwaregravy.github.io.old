---
layout: post
title: "Jekyll on Github"
date: 2013-08-04 17:58
category: 
tags: [jekyll]
---
{% include JB/setup %}

Struggling with Jekyll 
===

I started trying to get this post going using Octopress, but couldn't get it running on github. I followed the instructions line for line, restarted and restarted again. Failure.
Each time I pushed github would send me a message that my blog had failed to build. 

I decided there was a missing link and so switched to straight Jekyll. Again, failure.

Missing links so far:

* Github uses [redcarpet](https://github.com/nono/Jekyll-plugins) which is not the default. Add `markdown: redcarpet` to your `_config.yml` [Thanks SO](http://stackoverflow.com/questions/10759577/underscore-issues-jekyll-redcarpet-github-flavored-markdown)
* Remove things in the \_drafts folder
* Remove the examples under \_posts
* I used the twitter theme and had to apply [this](https://github.com/plusjade/jekyll-bootstrap/pull/74) patch manually


