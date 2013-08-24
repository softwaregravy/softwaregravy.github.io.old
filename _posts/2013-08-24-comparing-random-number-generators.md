---
layout: post
title: "Comparing Performance of Random number Generators"
description: ""
category: Rails
tags: [rails, performance]
github-issue-id: 5
---
{% include JB/setup %}

I am writing a program where I need to create random numbers. Potentially a lot of random numbers, and they must be unique. I will be putting them in my database so I'm using a unique constraint there, but for performance reasons on this API I really never want to get a collision. 

So "how fast do different generators work?", I wondered. Here's some really anecdotal, inconclusive results for how 2 different libraries perform. I'm testing methods from [UUIDTools](https://github.com/sporkmonger/uuidtools) and Ruby's [SecureRandom](http://www.ruby-doc.org/stdlib-1.9.3/libdoc/securerandom/rdoc/SecureRandom.html). 

Here are the results, read into them what you will.

```ruby
1.9.3p448 :034 > Benchmark.measure { 10000.times { UUIDTools::UUID.timestamp_create }}
 =>   0.310000   0.000000   0.310000 (  0.318563)

1.9.3p448 :035 > Benchmark.measure { 10000.times { UUIDTools::UUID.random_create }}
 =>   0.640000   0.010000   0.650000 (  0.673812)

1.9.3p448 :036 > Benchmark.measure { 10000.times { UUIDTools::UUID.md5_create(UUIDTools::UUID_DNS_NAMESPACE, "www.widgets.com") }}
 =>   0.930000   0.010000   0.940000 (  0.959783)

1.9.3p448 :037 > Benchmark.measure { 10000.times { UUIDTools::UUID.sha1_create(UUIDTools::UUID_DNS_NAMESPACE, "www.widgets.com") }}
 =>   0.940000   0.010000   0.950000 (  1.007404)

1.9.3p448 :038 > Benchmark.measure { 10000.times { SecureRandom.hex }}
 =>   0.050000   0.000000   0.050000 (  0.060006)

1.9.3p448 :039 > Benchmark.measure { 10000.times { SecureRandom.base64 }}
 =>   0.120000   0.000000   0.120000 (  0.124282)

1.9.3p448 :040 > Benchmark.measure { 10000.times { SecureRandom.urlsafe_base64 }}
 =>   0.130000   0.010000   0.140000 (  0.136464)

1.9.3p448 :041 > Benchmark.measure { 10000.times { SecureRandom.uuid }}
 =>   0.110000   0.000000   0.110000 (  0.113453)
```

I'm going with `SecureRandom` and may not use UUIDTools in the future (I'm using it another project)
