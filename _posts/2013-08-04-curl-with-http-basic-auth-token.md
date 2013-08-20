---
layout: post
title: "Curl with http basic auth token"
description: ""
category: 
tags: []
---
{% include JB/setup %}

Was trying to send a token on HTTP Basic Auth using a token. Took me a while to get it just right.

```bash
curl -i localhost:3000/api/customer_records.json -H "Authorization: Token token=\"122f20851e775438d5bf283a24XXXXX\""
```


