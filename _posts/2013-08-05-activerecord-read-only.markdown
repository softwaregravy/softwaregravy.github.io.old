---
layout: post
title: "ActiveRecord Read Only"
date: 2013-08-05 14:19
categories: [Rails]
tags: [ActiveRecord, Rails]
github-issue-id: 1
---

I'm creating a model in Rails which I need to be read only once created. More specifically, I want to make sure it gets created and then is frozen and immutable.

My plan was to just add a `before_update` hook which always fails. Something like:

Then I thought, there's gotta be a better way. Did some digging, and found the `readonly?` method on ActiveRecord::Base. Decided to give it a try.

```ruby
class ReadOnlyModel < ActiveRecord::Base
  def readonly?
    true
  end
end
```


Unfortunately, this prevents creation as well. 

Going back and trying out my first solution produces the desired results, though it's not really the cleanest since I'm attaching my error to the id. 

Here's my final result I'm going with:

``` ruby
class ReadOnlyModel < ActiveRecord::Base
  before_validation(on: :update) do
    errors.add(:id, "Model is readonly")
  end
```

Anywone have better suggestions?

