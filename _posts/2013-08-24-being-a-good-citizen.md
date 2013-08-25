---
layout: post
title: "Being a good citizen"
description: ""
category: Rails
tags: [rails, so]
github-issue-id: 6
---
{% include JB/setup %}

I just found an [SO Question](http://stackoverflow.com/questions/2134188/validate-presence-of-one-field-or-another-xor). I wanted a quick validation on how I was creating an XOR validation on 2 fields. (I was doing it right, I just like to know I'm doing it as simply as possible.)

While I was looking at the post I updated it to match the Rails 3 errors api and also to use more concise syntax on the validations. I rely on Google and SO so much, I love being able to contribute back, even if in a small way.

In case I forget again, here's XORing 2 fields in a validation.

```ruby
class AvailabilitySearch < ActiveRecord::Base
  validate :room_class_xor_property

  private
  def room_class_xor_property 
    if !(room_class_id.blank? ^ property_id.blank?)
      errors.add(:base, "Specify room_class_id or property_id, not both")
    end 
  end 
end
```

Of coure, it doesn't count until it's tested

```ruby
it "should require either room_class_id or property_id" do  
  dates = {:start_date => 2.days.from_now, :end_date => 4.days.from_now}
  AvailabilitySearch.new(dates).should_not be_valid
  AvailabilitySearch.new(dates.merge(:room_class_id => 1)).should be_valid
  AvailabilitySearch.new(dates.merge(:property_id => 1)).should be_valid
  AvailabilitySearch.new(dates.merge(:room_class_id => 1, :property_id => 1)).should_not be_valid
end 
```
