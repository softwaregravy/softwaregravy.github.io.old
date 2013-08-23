---
layout: post
title: "Speeding up my Specs"
description: ""
category: Rails
tags: [ruby, rails, rspec]
github-issue-id: 4
---
{% include JB/setup %}

I found [this article](http://developingandstuff.blogspot.com/2013/08/speed-test-ruby-193-vs-193-railsexpress.html) which lead me to [this other one](http://developingandstuff.blogspot.de/2013/08/tuning-your-ruby-gc-for-fun-and-profit.html) and was inspired to give it a shot.

I'm trying this out on a work project of roughly 2500 specs. I'm just running `time rspec spec` each time.

Before:

```
Finished in 3 minutes 4.72 seconds
2524 examples, 0 failures, 8 pending
Coverage report generated for RSpec to /workspace/thinknear/ventura/coverage. 4946 / 5333 LOC (92.74%) covered.
rspec spec  183.60s user 4.35s system 93% cpu 3:21.68 total
```

Copy-paste from blog:

```
export RUBY_HEAP_MIN_SLOTS=2000000
export RUBY_HEAP_SLOTS_INCREMENT=500000
export RUBY_HEAP_SLOTS_GROWTH_FACTOR=1
export RUBY_GC_MALLOC_LIMIT=70000000
export RUBY_HEAP_FREE_MIN=100000
```

After:

```
Finished in 2 minutes 32.96 seconds
2524 examples, 0 failures, 8 pending
Coverage report generated for RSpec to /workspace/thinknear/ventura/coverage. 4946 / 5333 LOC (92.74%) covered.
rspec spec  145.34s user 4.60s system 91% cpu 2:43.60 total
```

Looks pretty awesome!

Back of the envelope on the 1 sample size shows me with a 20% performance increase in speed.


