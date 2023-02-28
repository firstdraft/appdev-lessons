# Technical Setup Part 1: Accounts and Gitpod

## Get a GitHub account

Sign up for a free GitHub account at [github.com/join](https://github.com/join){:target="_blank"}
    
I recommend using your `.edu` email address, as that will qualify you for some discounts and coupons that you might want to use later. Remember to verify your email address after signing up.

If you already have a GitHub account, I recommend making a new one for this class, because some of the tools that we use will ask for permission to view _all_ of your repositories. If you have access to e.g. private work repositories, then you should make a new account and keep things separate.

<!-- ![](assets/technical-setup/1-github-join.png)

![](assets/technical-setup/2-github-plan.png)

![](assets/technical-setup/3-github-survey.png)

![](assets/technical-setup/4-github-complete.png)

![](assets/technical-setup/5-github-verify-email.png) -->

![file](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1677020490/1-github-join_qnfiek.png)

![file](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1677020490/2-github-plan_mkpjii.png)

![file](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1677020490/3-github-survey_btnmpe.png)

![file](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1677020489/4-github-complete_r4sfvp.png)

![file](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1677020490/5-github-verify-email_anezs3.png)


## Get a Heroku account

Sign up for a free Heroku account at [signup.heroku.com](https://signup.heroku.com/){:target="_blank"}

If asked what your primary development language is, say Ruby. You can use any one of your email addresses, but remember to verify it.

<!-- ![](assets/technical-setup/6-heroku-join.png)

![](assets/technical-setup/7-heroku-verify-email.png)

![](assets/technical-setup/8-heroku-welcome.png) -->

![file](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1677020563/6-heroku-join_ejfe1z.png)

![file](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1677020562/7-heroku-verify-email_tvjyc2.png)

![file](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1677020562/8-heroku-welcome_wwcn8v.png)

## GitHub and Heroku readings

While you're waiting for everyone to finish creating accounts, read up on GitHub and Heroku. Think of question:

 - Read about GitHub: [http://bit.ly/2skLlYx](http://bit.ly/2skLlYx){:target="_blank"}
 - Read about Heroku: [http://bit.ly/2uLVTAP](http://bit.ly/2uLVTAP){:target="_blank"}

## Gitpod

One of the most painful parts of learning how to program, in the old days, was simply setting up your computer to be able to write and run code. At a minimum, we needed to install:

  - An application to write your code with. Something like Microsoft Word is not be ideal for writing code, since code needs to be _plain text_ (just a series of characters in a file, nothing else) for the computer to understand it. Word is designed to write _rich text_ (for humans) with fonts, colors, sizes, margins, layouts, etc.

<aside markdown="1">
Computers come bundled with some plain text editors (Notepad, TextEdit, etc) but they are very basic. We would instead prefer to use powerful tools specifically designed for writing code with like Microsoft's VSCode or JetBrains' RubyMine.
</aside>

  - Ruby itself. Writing code is not useful on its own if we don't have something to run it with; just like we need a browser installed to interpret `.html` files we need Excel installed to interpret `.xls` files, and we need Photoshop installed to interpret `.ps` files, we need Ruby installed in order to interpret the `.rb` files that we write.

<aside markdown="1">
Not only do we need Ruby, we need the correct _version_ installed. If your computer happened to come with an older version, upgrading to a newer version could be complicated — especially if some other application you use depends on the older version.
</aside>

There are so many different combinations of hardware, operating systems, previously installed software, permission levels (for example if you are using a work-owned computer), that just getting these things installed would often stop you before you started writing your first program. We can't allow that!

Instead, we're going to use a write our code using a _cloud_ computer. "Cloud" just means that it's a computer that's sitting in someone's warehouse somewhere, and we rent it from them. It already has all of the software that we need installed on it, and we access it through our browsers. No muss, no fuss!

<aside markdown="1">
A warehouse full of computers that people rent and connect to via the internet is called a "data center". Some data centers have their own power plants, and some are even earthquake-proofed.
</aside>

Gitpod.io is a great new service that provides instantaneous, full-fledged cloud development environments from any codebase that is on GitHub.com — which is great, because we (and 98% of other teams) use GitHub to store all of our projects, homeworks, etc. The text editor they provide is based on Microsoft's VSCode — my editor of choice. It will have the exact right version of Ruby, Rails, and everything else we need. And they have a very generous free tier. Great!

### Getting Started With Gitpod

  1. Sign up for a [Gitpod.io](https://www.gitpod.io) account. It will ask you to sign in using your GitHub account.
  1. We will create a **workspace** for each project that we work on. Each workspace is based on a GitHub **repository** (i.e., a folder with some code in it; a.k.a., **repo**).

      - For example, here is a repository: [https://github.com/appdev-projects/helloruby](https://github.com/appdev-projects/helloruby)

  1. To create a Gitpod workspace based on a repo, in the address bar of your browser enter **https\://gitpod.io/#** and then the URL of the repo. For example,

      - **https\://gitpod.io/#https\://github.com/appdev-projects/helloruby**

  1. This creates a blank, brand-new computer. This is not a simple interactive terminal, nor is it an HTML application like we made for our early Rock, Paper, Scissors project. But Ruby _is_ installed on this computer. 

<aside markdown="1">
To make the process of opening a workspace with **https\://gitpod.io/#** easier, [Gitpod has a browser extension](https://www.gitpod.io/docs/20_browser_extension/) that you can install if you want to.
</aside>

Typically, we will assign you a Gitpod project in Canvas. The assignment will include a button that says "Load assignment in a new window". When you click on that button, it will create a fork (i.e. a copy) of the repository (i.e. the folder of code) on your own GitHub account. More on those technical set up steps [here](https://learn.firstdraft.com/lessons/29){:target="_blank"}, and for saving work on github [here](https://learn.firstdraft.com/lessons/30){:target="_blank"}.
