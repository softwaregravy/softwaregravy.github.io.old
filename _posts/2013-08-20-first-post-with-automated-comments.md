---
layout: post
title: "First Post With Automated Comments"
description: ""
category: General
tags: [testing]
github-issue-id: 3
---
{% include JB/setup %}

This is my first post created with my rake script which automatically created a github issue. 

I'm using Jekyll. Here's how I set it up.

## Setup

1. We will use <https://github.com/hit9/petal> to handle the actual commenting. Create an app on github as per petal docs.
2. Put the petal code in `_includes/custom/comments`
3. As per petal directions, sub out the repo name for your repo on github where we're going to create the comments. But use `{ { page.github-issue-id } }` for the issue id (no spaces between curly braces)
4. Create a Personal Access Token on github 
5. Install gem octokit (or add it to your Gemfile)
6. Update your Rakefile to create an issue upon post creation, and put the issue id in the post header
 - I put my token in a file (and added it to .gitignore)
 - make the following modifications to your Rakefile

```ruby
# at the top 
require 'octokit'

GITHUB_USER = "softwaregravy"
GITHUB_REPO = "softwaregravy/softwaregravy.github.io"
GITHUB_ACCESS_TOKEN = File.open(".github_token", "r").readline.strip
...
# then inside the :post task
client = Octokit::Client.new(:login => GITHUB_USER, :oauth_token => GITHUB_ACCESS_TOKEN)
issue = client.create_issue(GITHUB_REPO, title, "")
issue_id = issue.number
...
# then add the id to the post header
post.puts "github-issue-id: #{issue_id}"
```

Now when you create a post, you also create a comment thread on github -- no manual intervention required.

