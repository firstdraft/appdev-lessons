# AD2 Day 1 Recording

**BENP: Document based on first 30 minutes of modified descript transcription of AD2 WS 2023 Day 1 recording. Slides from [here](https://firstdraft.slides.com/raghubetina/appdev2-day1?token=dI0p5UEo)**

## Class Introduction, 00:00:00 to 00:10:41

- basic class introduction, getting to know each other

## Expectations, 00:10:41 to 00:13:30

In AD1, the objective was just get a taste of how development works. We got a sense of how things fit together, what's frontend, what's backend, what's deployment look like? We put something on our portfolio's and leanred how to "speak the language". 

In AD2, my assumption is you want to learn how to actually become a software developer. That means you could perhaps take a paid freelance gig by the end of this course! 

The primary objective in that case is for you to be able to Google for something that you need, for a project that you're building, and be able to make sense of what you find.

There's so much awesome information on the internet, but it's really hard for a beginner to make sense of what's what. And even with the skills that you learn after AD1, you don't quite have the vocabulary to interpret and understand all those amazing resources. Resources like StackOverflow, gem READMEs, the Rails guides, GoRails, etc.

There's so many things out there that I want you to be able to read and understand by the end of this course. Then you can go wherever you want after that! 

The training wheels are coming off. It's going to be a lot harder than AD1. We're going to go faster, cover more advanced material, and we're going to translate less. Rather than writing a chapter for every topic, we're going to send you to the primary source material and have you try to interpret it yourself.

## Approach 00:13:30 to 00:14:57

We're treating this course as a virtual apprenticeship. Some of the things that I want my apprentices to do is start a blog and write about what you're learning. Also we will subscribe to a newsletter that all professional Rails developers subscribe to. This is how I continue to stay on top of developments and learn and improve my own skills.

### Materials 

Unlike AD1, there will be some paid material. You might have to subscribe to Gitpod, since many AD2 students spend more than the 50 hours a month coding there. There are also paid online courses that you will be assigned. 

The total materials will be around $200 depending on what you decide to do during the course. But, I've tried to select things that you can refer to over and over again throughout your career.

Again, the objective is for you to be comfortable consuming the wide world of resources available outside of the AD1 and AD2 materials.

### Plan 00:14:57 to 00:18:14

Here's our plan for the course

#### Leveling Up

First, we're going to level up our Rails and Ruby knowledge; we only scratched the surface in AD1, but there's so much more depth to get to!

In AD1, we ended by generating a `draft:resource`, which automatically wrote all the code that we spent the first chunk of the course learning how to write. In AD2, we're going to level up that, and learn how to make it match the expectations of a real industrial grade application.

We're also going to spend some time learning how to write automated tests. In AD1, you ran `rails grade` to check whether your app was working. _We_ (the teachers) wrote those automated tests for you! 

Writing your own automated tests is crucial when you're building your own stuff and you want to make sure that you're meeting your client's expectations. Also, as you add features, tests ensure you're not breaking any old stuff. 

#### Workflow

After we level up our Ruby and Rails, we're going to start to learn some more workflow-type things. We're going to get a lot more familiar with `git`. In AD1, we just made lots of commits so we wouldn't lose work. That's a single developer workflow, but the real power of `git` is how it allows teams to work together.

Learning about `git` branches, pull requests, and other abilities will let us start to code review.

This is a workflow that I want you to become familiar with, even when you're interacting with teams that you manage. This is how we ensure the quality of code that we write.

Code review prevents bugs from creeping in. Every developer has to run the code that they write by the rest of the team before it gets merged into the code base that's on our production server. But most importantly, that gives us an opportunity to learn from each other.

#### Building Apps 00:18:00 to 00:20:30

Finally, we're going to spend most of the time just practicing building apps. This will give you practice with the things we learn about leveling up and workflow. If you can do that, you'll be able to build pretty legit stuff. 

Recall the final project app from AD1: [Photogram](https://photogram-final.matchthetarget.com/). It's a fully functional social network. You can sign in, follow people, look at a home feed, see posts, etc. 

**BENP: insert GIF here of PG final?**

But, there are a few issues. Number one, it looks terrible! Also, every time I click on something, it does a full page refresh and takes me back up to the top. Not the greatest user experience. 

In AD2 two, we want to learn how to keep the same functionality with more concise and professional code. In the end, we want to build a [new version of Photogram](https://pg-ajax-1.matchthetarget.com/users/sign_in).

First of all, there's Bootstrap here, so its CSS is a lot better, and we're going to be using a lot more CSS in AD2. Most importantly, look at a feed: I can go scroll down, click the like button, and the page doesn't refresh!

**BENP: insert GIF here of PG AJAX 1?**

My click updated the record back in the database, but it didn't have that janky user experience of refreshing the page. That's known as AJAX. In order to get there, we have to learn JavaScript, and a whole bunch of other stuff. 

Once we get to this point, then you can start to take freelance projects and do legitimate app building. 

#### Fork in the Road 00:20:30 to 00:21:30

After building an industrial-grade Photogram social network, we have what's called the "fork in the road", and you all get to pick your own independent study track.

Some people may go deep on a project. Maybe you have a startup in mind, maybe you want to level up your final project from AD1. 

The idea is, to take all the skills you learned in the first half fo the course, and, with our mentorship, build something very solid. That means adding tests, authentication, and more.

A lot of people are interested in getting a taste of iOS and Android development. If you want to take that path, then there's a whole other set of learning to do; splitting up the backend and frontend using React and React Native.

#### Along the way 00:21:30 to 00:23:00

Along the way, we're going to pick up a whole bunch of workflow-related things. We'll talk about Heroku, and other strategies for deploying our app.

In addition to code review, we'll discuss review apps and continuous integration. These are all ways that make it much more efficient to collaborate with designers and other non-technical stakeholders on your team, including clients, QA, etc. Also, performance and error monitoring are essential things to include anytime you deploy an app to real users.

We already learned a little bit about authentication (sign up, sign in, sign off) and authorization (hide and show using conditionals depending on user). We did that in AD1, but there's much more robust ways that we're going to have to learn now.

## TIL Journal 00:23:00 to 00:26:00

**BENP: below partially copied from https://canvas.uchicago.edu/courses/47618/assignments/523614**

Keeping a learning journal is extremely valuable for software developers, for many reasons:

 - Writing about what you’re doing helps clarify and internalize it.
 - The post serves as documentation for the code, for teammates and your future self.
 - When you inevitably have to do the same task again six months or two years later, you’ve written a cheat sheet for yourself.
 - It looks great to prospective employers, demonstrating both writing and technical ability, among other things.

Here is [Jelani's learning journal](https://jelani.dev/), as a great example.

We call it a "learning journal" (or "Today I Learned", or TIL for short) instead of a "blog" deliberately. A blog seems like the posts should be polished enough to share with the world, whereas a TIL is a place to jot down brief notes mostly for your own benefit.

We're going to use [dev.to](https://dev.to/) for our blogs, for now. (In the future you can consider building your own blog — that would be a good Rails exercise. Or you can use [GitHub Pages](https://pages.github.com/), a free hosting product from GitHub for static websites.)

 - Sign up for a [dev.to account](https://dev.to/enter) — I recommend signing in with GitHub so that you don't have to make up yet another password.

Think of this as a place to take notes, where I and the other instructors are able to leave comments to reinforce/clarify what you are writing about. Start using it even today to take notes about what you learn!

## Subscribe to Ruby Weekly 00:26:00 to 00:32:00 

There are two more things to get started today. 

First, subscribe to the [Ruby Weekly email newsletter](https://rubyweekly.com/) (or, as I prefer, subscribe to the RSS feed).

Glance over it each week and see if anything intrigues you; click through if so. Quite often the articles cover beginner/intermediate-level material, and that's what interests me most. I usually skip the advanced stuff.

As a developer, this is:

 - how I learn about new libraries that are gaining traction
 - how I learn that old libraries received significant updates
 - in general, stay on top of trends in the Ruby community
 - incidentally, the only way that companies can ever successfully advertise to me, either products or for recruitment

Every language has a similar newsletter; it's worth getting a feel for them.

## Improve your Ruby with Exercism 00:32:00 to 

Besides Ruby Weekly, let’s level up our Ruby skills with Exercism.io, a wonderful non-profit project. It’s a community for leveling up programming skills through solving problems, discussion, and mentorship.

Sadly, the demand for Ruby mentorship overwhelmed the supply of mentors, so for the time being you may not receive timely code reviews; but 1) we can still review each other, and 2) the previous solutions and discussions about them are public and still incredibly useful for learning various ways to solve a problem with Ruby.

Furthermore, one of the most valuable things about Exercism is when it comes time to learn new languages (like JavaScript in a couple of weeks). A great way to learn new syntaxes is to solve the same problems that you’ve already solved before in a familiar language.

### One-time Setup

 1. Sign up for an account at [exercism.io](https://exercism.io/) (I suggest you use your Github account again for this).
 
 1. Join the [Ruby Track](https://exercism.org/tracks/ruby).
 
 1. Complete the "Hello World" introductory exercise using the in-browser editor.
 
 1. Once "Hello World" is complete, the "Lasagna" exercise should be unlocked. You can see which exercises are unlocked from the track overview
 
 1. Complete "Lasagna". There are helpful lessons and hints available in the sidebar.
 
 1. Once you've unlocked it, try [the "Log line Parser" exercise](https://exercism.org/tracks/ruby/exercises/log-line-parser).
 
 1. It may be useful to [create a throwaway Ruby workspace in Gitpod](https://gitpod.io/#https://github.com/appdev-projects/base-ruby), so you can use IRB or print things more easily.
 
 1. Start reading the automated tests and pay attention to how they are written — soon you’ll have to write tests yourself.

 1. Once you've submitted a working solution, the best part: view Community Solutions.
    - [Here are my solutions](https://exercism.org/tracks/ruby/exercises/log-line-parser/solutions/demostudent17). There are two iterations — check out both.
    - Look at a few of the most-starred [Community Solutions](https://exercism.org/tracks/ruby/exercises/log-line-parser/solutions).
    - How do they compare to your solution? Did you learn anything from them? **If so, write up a quick note in your TIL blog.**

 1. Try doing a few Exercism problems each week to keep improving your Ruby skills continuously. 