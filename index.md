---
title: "AD1"
author: "Ben + Raghu"
description: "This book covers the AD1 course at UChicago"
url: # 'https\://bookdown.org/john/awesome/'
github-repo: "bpurinton/appdev-textbook"
site: bookdown::bookdown_site 
documentclass: book
favicon: "assets/favicon.ico"
---

# Preface {-}

This is the basic outline of a "Lesson" in the planned LMS app, including the syntax for LTI placement and quiz questions

```ruby
class Person
	 attr_accessor :first_name, :last_name
	 
	 def full_name
	   "#{first_name} #{last_name}"
	 end
end
```

- Bullets
- More `bullets`

A paragraph.

LTI{Launch the tool}(https://lti-provider-example.herokuapp.com/lti_tool)[test]{secret}(20)[foo]{400}

- Bullets
- More bullets

LTI{ }(https://lti-provider-example.herokuapp.com/lti_tool)[test]{secret}(10)[bar]

## Choose one {-}

- First bullet point is the question itself?
- First option
    - This is not correct because of xyz reason
- Second option
    - This is not correct because of xyz reason
    - Also not correct because of abc reason
- Third option
    - That's right! Because of xyz reason
- Fourth option
    - This is not correct because of xyz reason

{: .choose_best #bin points="30" answer="3" }

## Choose all that apply {-}

- First bullet point is the question itself?
- First option
    - This is not correct because of xyz reason
- Second option
    - This is not correct because of xyz reason
    - Also not correct because of abc reason
- Third option
    - That's right! Because of xyz reason
- Fourth option
    - That's right! Because of xyz reason
{: .choose_all #baz points="30" answer="[3, 4]" }