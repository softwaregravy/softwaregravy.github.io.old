---
layout: post
title: "Jekyll on Github"
date: 2013-08-04 17:58
categories: [General]
tags: [jekyll]
---

I really struggled to get going with jekyll

Like, I really struggled. Being a software engineer by trade, I'm ashamed how many different things I tried and failed at. All I wanted was a nice little blog that worked with gibhub markdown format.

In the end I just

1. Used http://jekyllbootstrap.com/ to get started
2. Added a Gemfile with `gem 'github-pages'` in it
3. Changed themes

A killer problem for me is that the default theme for jekyll bootstrap (the twitter one) has some sort of css conflict that kills syntax highlighting. I'm sure it would be easy to fix if I was any good with css.

Anyway, after that, you just push to github. No need for any jekyll operations. (Just `jekyll serve -w` to preview.)
