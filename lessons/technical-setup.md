# Technical Setup

- Notes:

  - These steps are done in [RPS HTML][Rock, Paper, Scissors HTML] and [String][String]

  - This is a place to collect dedicated how-to-guides to refer students back to
  
  - Dedicated video tutorials would be helpful here as well

## Setting Up Accounts 

- Notes:

  - Copied from [`day-2-notes.md`](https://github.com/firstdraft/appdev-chapters/blob/benp-edits/day-2-notes.md){target="_blank"}

### Get a GitHub account

Sign up for a free GitHub account at [github.com/join](https://github.com/join){target="_blank"}
    
I recommend using your `.edu` email address, as that will qualify you for some discounts and coupons that you might want to use later. Remember to verify your email address after signing up.

If you already have a GitHub account, I recommend making a new one for this class, because some of the tools that we use will ask for permission to view _all_ of your repositories. If you have access to e.g. private work repositories, then you should make a new account and keep things separate.

![](assets/technical-setup/1-github-join.png)

![](assets/technical-setup/2-github-plan.png)

![](assets/technical-setup/3-github-survey.png)

![](assets/technical-setup/4-github-complete.png)

![](assets/technical-setup/5-github-verify-email.png)

### Get a Heroku account

Sign up for a free Heroku account at [signup.heroku.com](https://signup.heroku.com/){target="_blank"}

If asked what your primary development language is, say Ruby. You can use any one of your email addresses, but remember to verify it.

![](assets/technical-setup/6-heroku-join.png)

![](assets/technical-setup/7-heroku-verify-email.png)

![](assets/technical-setup/8-heroku-welcome.png)

### GitHub and Heroku readings

While you're waiting for everyone to finish creating accounts, read up on GitHub and Heroku. Think of question:

 - Read about GitHub: [http://bit.ly/2skLlYx](http://bit.ly/2skLlYx){target="_blank"}
 - Read about Heroku: [http://bit.ly/2uLVTAP](http://bit.ly/2uLVTAP){target="_blank"}

## GitPod

- Notes:

  - can use [RPS HTML][Rock, Paper, Scissors HTML] as example
  - should include forking, workspace layout, bin/server, tab management
  - could be chance to talk about file structures and terminal

### Getting Started With Gitpod

- Notes:

  - Copied from [`getting-started-with-gitpod.md`](https://github.com/firstdraft/appdev-chapters/blob/benp-edits/getting-started-with-gitpod.md){target="_blank"}

One of the most painful parts of learning how to program, in the old days, was simply setting up your computer to be able to write and run code. At a minimum, we needed to install:

- An application to write your code with. Something like Microsoft Word is not be ideal for writing code, since code needs to be _plain text_ (just a series of characters in a file, nothing else) for the computer to understand it. Word is designed to write _rich text_ (for humans) with fonts, colors, sizes, margins, layouts, etc.

  Computers come bundled with some plain text editors (Notepad, TextEdit, etc) but they are very basic. We would instead prefer to use powerful tools specifically designed for writing code with like Microsoft's VSCode or JetBrains' RubyMine.

- Ruby itself. Writing code is not useful on its own if we don't have something to run it with; just like we need a browser installed to interpret `.html` files we need Excel installed to interpret `.xls` files, and we need Photoshop installed to interpret `.ps` files, we need Ruby installed in order to interpret the `.rb` files that we write.

  Not only that, we need the correct _version_ installed. If your computer happened to come with an older version, upgrading to a newer version could be complicated — especially if some other application you use depends on the older version.

There are so many different combinations of hardware, operating systems, previously installed software, permission levels (for example if you are using a work-owned computer), that just getting these things installed would often stop you before you started writing your first program. We can't allow that!

Instead, we're going to use a write our code using a _cloud_ computer. "Cloud" just means that it's a computer that's sitting in someone's warehouse[^datacenter] somewhere, and we rent it from them. It already has all of the software that we need installed on it, and we access it through our browsers. No muss, no fuss!

[^datacenter]: A warehouse full of computers that people rent and connect to via the internet is called a "data center". Some data centers have their own power plants, and some are even earthquake-proofed.

Gitpod.io is a great new service that provides instantaneous, full-fledged cloud development environments from any codebase that is on GitHub.com — which is great, because we (and 98% of other teams) use GitHub to store all of our projects, homeworks, etc. The text editor they provide is based on Microsoft's VSCode — my editor of choice. It will have the exact right version of Ruby, Rails, and everything else we need. And they have a very generous free tier. Great!

1.  Sign up for a [Gitpod.io](https://www.gitpod.io) account. It will ask you to sign in using your GitHub account.
2.  We will create a **workspace** for each project that we work on. Each workspace is based on a GitHub **repository** (i.e., a folder with some code in it).

    For example, here is a repository:

    [https://github.com/appdev-projects/helloruby](https://github.com/appdev-projects/helloruby)

3.  To create a Gitpod workspace based on a repo, in the address bar of your browser enter `https://gitpod.io/#` and then the URL of the repo. For example,

    [https://gitpod.io/#https://github.com/appdev-projects/helloruby](https://gitpod.io/#https://github.com/appdev-projects/helloruby)

4.  To make that process easier, [Gitpod has a browser extension](https://www.gitpod.io/docs/20_browser_extension/) that you can install if you want to.

5.  Typically, we will assign you a project in Canvas. The assignment will include a button that says "Load assignment in a new window". When you click on that button, it will create a fork (i.e. a copy) of the repository (i.e. the folder of code) on your own GitHub account.

    You will then create a Gitpod workspace[^workspace] based on _your_ fork, so that you can save the work that you do back to your own GitHub account. A button to create your Gitpod workspace will appear within the assignment, so usually all you need to do is click on it after clicking "Load assignment in a new window". And then you can get right to work, with the exact right version of all of the project's dependencies ready to go!

[^workspace]: Gitpod will delete an inactive workspace after **14 days**. If you want to save the changes you've made for longer, you can "pin" a workspace in Gitpod which will prevent it from being deleted. Even better, you can [push your changes to Github](https://chapters.firstdraft.com/chapters/839#push-to-github).


### Forcing Chrome to "Hard" Refresh

- Notes: 

  - Copied from [`hard-reload.md`](https://github.com/firstdraft/appdev-chapters/blob/benp-edits/hard-reload.md){target="_blank"}

Sometimes, when we update a CSS stylesheet, our page appears not to change. This is especially frequent when we're working on static HTML files in the `public/` folder.

The cause is usually Chrome's aggressive "caching", i.e. re-using static assets that it has already downloaded (for performance reasons). If we refresh an HTML page that we've updated, Chrome won't necessarily also refresh all `<link>`ed CSS files — unless we ask it to by "hard" refreshing.

To do so:

 1. Open the Dev Tools...
    - from the `View > Developer` menu
    - or right-click on any element and `Inspect`
    - or press <kbd>F12</kbd>
    - or <kbd>Ctrl</kbd>`+`<kbd>Shift</kbd>`+`<kbd>J</kbd> (on Windows) or <kbd>Option</kbd>`+`<kbd>Command</kbd>`+`<kbd>J</kbd> (on Mac)
 2. **Right-click** on the refresh button.
 3. Select "Empty cache and hard reload".

Open Dev Tools:

![](assets/technical-setup/hard-refresh-dev-tools-2.png)

With Dev Tools open, "hard" refresh:

![](assets/technical-setup/hard-refresh-right-click-refresh-2.png)

Your HTML document should now have the latest CSS and any other linked assets (like images or javascripts).

### Gitpod keyboard shortcuts and other productivity tips

- Notes:

  - Copied from [`tips-and-tricks.md`](https://github.com/firstdraft/appdev-chapters/blob/benp-edits/tips-and-tricks.md){target="_blank"}

#### Important Terminal keystrokes to know

##### Jump to beginning of line

You can't use your mouse at the command line, so it's important to know how to move around quickly so you're not restricted to just using your arrows. Jump back to the beginning of the line with <kbd>Ctrl</kbd> + <kbd>A</kbd>:

![](assets/technical-setup/back-to-beginning.gif)

##### Jump to end of line

Mac OS, Windows: <kbd>Ctrl</kbd> + <kbd>E</kbd>

![](assets/technical-setup/back-to-end.gif)

##### Up and down arrows to scroll through your history

Use your up and down arrows to scroll through your command history so that you don't have to re-type your commands over and over.

![](assets/technical-setup/previous-terminal-command.gif)

##### Clear Terminal

Mac OS: <kbd>Command</kbd> + <kbd>K</kbd>

Windows: Disabled by default[^windows-clear]

![](assets/technical-setup/clear_terminal.gif)


[^windows-clear]: A recent Gitpod update removed this keyboard shortcut for Windows, so you'll need to configure it yourself.

From the menu open Preferences and select Keyboard shortcuts.

![](assets/technical-setup/gitpod-keyboard-shortcuts.png)

Then search for "terminal clear" in the search bar and click the plus icon to the left of it.

![](assets/technical-setup/gitpod-clear-terminal.png)

Finally, type <kbd>Ctrl</kbd> + <kbd>K</kbd> and <kbd>Enter</kbd> to confirm.

![](assets/technical-setup/gitpod-ctrl-k.png)

##### Interrupt command

If something goes wrong with a terminal program (i.e. you made a typo, a program gets stuck in an infinite loop, etc), you can generally interrupt it with <kbd>Ctrl</kbd> + <kbd>C</kbd>:

![](assets/technical-setup/ctrl-c-to-quit.gif)

##### Q to exit

When the output of a terminal command is too tall for a terminal tab to display at once, it paginates. Press <kbd>Space</kbd> to step through it one page at a time, or <kbd>Q</kbd> to quit and get back to the terminal prompt so that you can execute your next command.

Mac OS, Windows: <kbd>Q</kbd>

![](assets/technical-setup/q-to-exit.gif)

#### Editor keyboard shortcuts

##### Command Palette

The most important thing to memorize is how to open the **Command Palette**, which will allow you to fuzzy search within for all other commands. If the command has a keyboard shortcut mapped to it, the shortcut will be displayed to the right. This is the best way to learn the keyboard shortcuts for the commands that you use most frequently.

Mac OS: <kbd>Command</kbd> + <kbd>Shift</kbd> + <kbd>P</kbd>

Windows: <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>P</kbd>

![](assets/technical-setup/gitpod-command-palette.gif)

##### Quick open file

To quickly jump to a file:

Mac OS: <kbd>Command</kbd> + <kbd>P</kbd>

Windows: <kbd>Ctrl</kbd> + <kbd>P</kbd>

And then fuzzily search for its name. For example, you could type "phco" to get to **ph**otos_**co**ntroller.rb and the list would quickly narrow to bring that file to the top of the list.

![](assets/technical-setup/open_file.gif)

##### Toggle Code Comment

To quickly comment a line of code, put your cursor on that line and then:

Mac OS: <kbd>Command</kbd> + <kbd>/</kbd>

Windows: <kbd>Ctrl</kbd> + <kbd>/</kbd>

You can also highlight multiple lines of code and comment/uncomment all of them at once.

![](assets/technical-setup/toggle-comment.gif)

##### Find (and replace)

Mac OS: <kbd>Command</kbd> + <kbd>F</kbd>

Windows: <kbd>Ctrl</kbd> + <kbd>F</kbd>

![](assets/technical-setup/find_and_replace.gif)

##### Find Next Selection

Mac OS: <kbd>Command</kbd> + <kbd>D</kbd>

Windows: <kbd>Ctrl</kbd> + <kbd>D</kbd>

![](assets/technical-setup/select_next.gif)

If you go too far by mistake, you can step backwards with <kbd>Command</kbd> + <kbd>U</kbd> or <kbd>Ctrl</kbd> + <kbd>U</kbd>.

##### Move line

Mac OS: <kbd>Option</kbd> + <kbd>&#11015;</kbd>

Windows: <kbd>Alt</kbd> + <kbd>&#11015;</kbd>

![](assets/technical-setup/move_line.gif)

##### Duplicate line

Mac OS: <kbd>Shift</kbd> + <kbd>Option</kbd> + <kbd>&#11015;</kbd>

Windows: <kbd>Shift</kbd> + <kbd>Alt</kbd> + <kbd>&#11015;</kbd>

![](assets/technical-setup/duplicate_line.gif)

##### Add/Remove Tab spaces for multiple lines

Mac OS: (<kbd>Shift</kbd>) + <kbd>Tab</kbd>

Windows: (<kbd>Shift</kbd>) + <kbd>Tab</kbd>

![](assets/technical-setup/tab-spacing.gif)

##### Add More Cursors

Mac OS: <kbd>Option</kbd> + Click

Windows: <kbd>Alt</kbd> + Click

![](assets/technical-setup/multiple-cursors.gif)

##### Embedded Ruby (ERB) Tag Toggle

Mac OS, Windows: <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>`</kbd>

![](assets/technical-setup/ERB-shortcut.gif)

##### Toggle Terminal Panel

Mac OS: <kbd>Command</kbd> + <kbd>J</kbd>

Windows: <kbd>Ctrl</kbd> + <kbd>J</kbd>

![](assets/technical-setup/toggle_terminal_view.gif)

##### Open New Terminal

Mac OS: <kbd>Ctrl</kbd> + <kbd>~</kbd> (i.e. <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>`</kbd>)

Windows: <kbd>Ctrl</kbd> + <kbd>~</kbd> (i.e. <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>`</kbd>)

![](assets/technical-setup/new_terminal.gif)



## Using Git to freely experiment and save work

- Notes:

  - Copied from [`using-git-to-experiement-and-save-work.md`](https://github.com/firstdraft/appdev-chapters/blob/benp-edits/using-git-to-experiement-and-save-work.md){target="_blank"}

### What Git is

[Git](https://en.wikipedia.org/wiki/Git) is an extremely powerful **version-control system** created by Linus Torvalds in 2005 for development of the Linux kernel, which is one of the largest open-source software projects in existence. It makes it possible for large numbers of contributors to work on various features, all within a single codebase (which could be comprised of hundreds or thousands of files).

Bitbucket, GitLab, and especially GitHub (all private companies) rode the rise of Git (the protocol) to become the center of the software development universe. All of these companies basically offer cloud-based storage for codebases using Git for version-control (we refer to these codebases as **repositories**), as well as a web-based interface for collaborating on them — following, commenting, etc.

### Why we care

In this course, we're going to use one simple but effective Git-based workflow to save versions of our work. This will allow us to freely experiment with different approaches, while never having to throw away code.

In all of our Rails apps, after you start the server, you can navigate to the address **/git** in your live application. If you're using Gitpod, the URL will look like:

    https://[YOUR GITPOD WORKSPACE URL].gitpod.io/git

That will open a page that looks like this:

![](assets/technical-setup/git-clean.png)

As soon as you make any changes to any of the code in the project, and refresh this page, the lines that you changed will appear:

![](assets/technical-setup/git-changes.png)

On the left, you see the code as it was previously; on the right, you see the new code. Lines added are highlighted in green, lines removed are highlighted in red.

Below, there are two things you can do: **commit** your changes on the left, and switch to a new **branch** on the right. When you hear the word "commit", think "snapshot". When you hear the word "branch", think "version".

A Git commit is a snapshot of _all_ of the folders and files in your project _at a particular time_. Since our files of code are all interdependent, it doesn't make sense to save versions of individual files — we need to know the _entire_ state of the project for a version to be useful.

Each branch ("version") is a series of commits ("snapshots").

The most important thing for you to remember is simple: **commit early and commit often**. As long as you are taking snapshots of your work at various points, it will always be easy to get back to a previous state in case you want to start over and explore a different approach.

To commit, enter a title for the snapshot (required), and, optionally, a longer description:

![](assets/technical-setup/git-commit.png)

After you commit, you will no longer have any pending changes:

![](assets/technical-setup/git-changes-committed.png)

If you edit your code again, then you can make further commits.

**Fundamentally, that's all you need to worry about: just make lots of commits as you work.**

The best time to commit is right after you just got something to work, before you start on your next experiment.

Remember: **ABC**: *Always Be Committing (ABC)*.

### Jumping back in time

In the History dialog at the bottom, you can see a list of all of the commits you've made. If you want to jump back in time to one of them, copy the 7 letter code (known as the "hash" of the commit; it is a unique identifier) in front of it into the "Branch off of" field above. Pick a name for a new version, and click "Create a new branch off of...".

It will snap all of the files in the project back to that point in time, and you can now make further commits along a new path — while still retaining all of your old commits on the old path.

![](assets/technical-setup/git-jump-back.png)

You can easily jump to any commit from any branch at any time — so feel free to experiment! Make a commit to save your current work, then jump back to a previous commit to try a different approach.

### Switch to a Different Branch

Have you gone back in time and decided your first attempt was better? Turn your attention to the "Existing Branches" panel on the right. This will list any branches your project has— `master` is the default starting branch. To switch to a different branch, click the blue double arrow button next to the name of the branch you want to switch to.

![](assets/technical-setup/git-switch-branch.png)

If you're ever unsure of what branch you're on, the top of the page should list "On branch \_\_\_".

### Push to GitHub

Gitpod workspaces are not permanent. Even if we make git commits, if the workspace is deleted so is all of our work! This is where GitHub comes in. We can push all of the commits we've made to our repository on GitHub where it will live forever. If our Gitpod workspace gets destroyed we can just re-create another one from the latest commit on GitHub!

Before you can push to GitHub, you need to give Gitpod access. Head over to the [Integrations under your account settings](https://gitpod.io/integrations) in Gitpod and make sure you check "public repos" and click "Update". 

![](assets/technical-setup/gitpod-integration-settings.png)

This should open a GitHub authorization dialogue.

**Make sure to click "Grant" next to the GitHub organization you created for class**

![](assets/technical-setup/gitpod-github-organization-permissions.png)

Now you should be all set to push your commits to GitHub!

## `rails grade`

- Notes:

  - manually checking work, rails grade, git commiting

### Getting automated feedback with rails grade

- Notes:

  - Copied from [`rails-grade.md`](https://github.com/firstdraft/appdev-chapters/blob/benp-edits/rails-grade.md){target="_blank"}

#### Join GitHub

If you haven't already, [sign up for a free GitHub account](https://github.com/join) (or sign in to yours if you already have one):

![](assets/technical-setup/join-github.png)

In this example screenshot, I chose a username of `demolearner1` — remember yours. Also, don't forget to check your email and verify the address you entered.

For now, think of GitHub like Dropbox-for-programmers; it's where we're going to store all of our code.

#### Create GitHub organization

To keep things organized, we're going to create a separate GitHub organization account for you to store your AppDev projects under (to keep them separate from the personal projects that you'll hopefully be building soon!).

Click the `+` on the right side of the navbar and select "New organization":

![](assets/technical-setup/new-organization.png)

Choose any name for the organization; most students choose `[YOUR USERNAME]-appdev`. In this example screenshot, I chose `demolearner1-appdev`:

![](assets/technical-setup/org-name.png)

You can "Skip" or "Finish" the rest of the screens:

![](assets/technical-setup/finish-org.png)

#### Login to Canvas

Open up the Assignments tab and make sure they're sorted by type.

![](assets/technical-setup/login-canvas.png)

Scroll down to the assignment you want to start and click the link that says 'Load [your assignment name] in a new window' (the name of the project will vary).

![](assets/technical-setup/load-assignment.png)

**_Before_ you click "Authorize", make sure to click the "Grant" button next to the organization that you created earlier.** Only then, click authorize to allow the firstdraft Grades application to access your account. 

![](assets/technical-setup/authorize-first-draft.png)

Select the name of your GitHub **organization** and submit the form.

![](assets/technical-setup/add-github-org-name.png)

The next screen will ask you to accept an invitation to a GitHub team. You can click the link on that screen to accept, or you'll have an invitation in your email inbox as well.

Once you've joined, you should see feedback that you're now a member of appdev-projects:

![](assets/technical-setup/github-joined-org-feedback.png)

#### Daily workflow

The stuff above about setting up your organization and permissions was just a one-time thing. From now on, you'll just head to Canvas and click "Load assignment in a new tab". You should see something like the following (the name of the project will vary):

![](assets/technical-setup/grade-setup-instructions.png)

We will automatically make a copy (a "fork", in GitHub parlance) of the repository under your new GitHub organization. Then, you can choose to either "Create new workspace in Gitpod" or head to your "Gitpod Dashboard" to view existing workspaces.

Either way, once you're in the workspace, we can get the project loaded up and try out the feedback feature. After the `bin/setup` script is done running, start working on the project to do whatever the instructions tell you. **When you're ready for feedback**, try a new command at a new Terminal prompt:

```
rails grade
```

You'll be asked for your access token; **copy-paste it carefully from the grades.firstdraft.com page that you loaded from Canvas**.

![](assets/technical-setup/gitpod-enter-token.png)

You should see output that looks like:

![](assets/technical-setup/gitpod-rails-grade.png)

Copy-paste the Results URL into a new tab, or click on it (but make sure it isn't truncated).

![](assets/technical-setup/gitpod-rails-grade-open.png)

![](assets/technical-setup/rails-grade-results.png)

**(Some projects aren't graded; in that case there may only be one dummy test listed.)**

You can click on one of the tests to get more feedback on what might have gone wrong:

![](assets/technical-setup/rails-grade-results-details.png)

In this case, the test expected to find an element with a class of `word_count` that contains the number 10, but instead it only found the content "Replace this string with your answer". 

You can click the "Examine Test" button to read the actual Ruby of the automated test; it's surprisingly readable. Ruby's testing libraries use method names that are supposed to make tests readable even for non-technical managers and clients. You can see specifically what flow is being tested and what inputs are being used and what the expected output is, and try to reproduce the issue in your own app manually using the same inputs.

You can run `rails grade` in your Terminal as many times as you want, and you will get a new updated build report each time. It will only report your highest score back to Canvas.

**Remember that your first job is always to make your app work as described and test it manually yourself. You should not rely exclusively on the automated tests; they are a terrible way to debug.**

### Fixing your organization permissions

- Notes:

  - Copied from [`fixing-your-organization-permissions.md`](https://github.com/firstdraft/appdev-chapters/blob/benp-edits/fixing-your-organization-permissions.md){target="_blank"}

Once upon a time, we all [created our own GitHub organizations](https://chapters.firstdraft.com/chapters/777#create-github-organization) to keep our classwork separate from our personal projects.

Since then, whenever we gave permission to a third-party (like Gitpod or grades.firstdraft.com) to access our GitHub accounts, we were supposed to remember to grant access to our organization too. **If you forgot to click "Grant" next to the organization that you created before you clicked "Authorize", you're going to run into problems.** Let's fix it.

Go to GitHub and sign in. In this example, I am signed in as the user `demolearner1`. Click on the user icon in the top-right and find "Settings":

![](assets/technical-setup/github-settings.jpg)

Next, click on "Organizations" in the left sidebar:

![](assets/technical-setup/github-orgs.jpg)

Find the organization that **_you_ created**. You likely picked a name like `[YOUR USERNAME]-appdev`:

![](assets/technical-setup/org-list.jpg)

Next, go to the Settings of the organization:

![](assets/technical-setup/find-org-settings.jpg)

In the left sidebar, find "Third-party access":

![](assets/technical-setup/third-party-access.jpg)

-   If it says that you approved both, then you are good to go and you can go to the next section.
-   If neither Cloud9 nor Grades appears in this list, click the "Remove restrictions" button instead and you can go to the next section.
-   If it says that access is Denied next to Cloud9 or Grades, then proceed.

![](assets/technical-setup/access-denied.jpg)

Click on whichever one you denied and Grant Access:

![](assets/technical-setup/grant-access.jpg)

You should see a message confirming that access has been granted:

![](assets/technical-setup/access-granted-flash.jpg)

Repeat for the other third-party app if necessary.

#### Make sure that you've accepted your team invitation

Visit [this page](https://github.com/appdev-projects) and make sure that you _don't_ have a banner across the top asking you to accept our team invitation. (This invitation was sent a while ago via email; if you've already accepted it, the banner won't appear.)

#### Launch an assignment from within Canvas

Head back to Canvas and click on whichever assignment you want to work on again **(don't just refresh it if you already had it up)**. You might be asked to enter your organization name — be sure to enter _your_ organization name, the one you created; not `appdev-projects`.

#### Resetting OAuth permissions to square one

If for some reason you need to make a single-sign-on provider (like GitHub, Twitter, or Facebook) "forget" that you ever authorized a third-party app, maybe because you don't use it anymore or maybe because you want to change the permissions that you gave it, you need to delete or revoke the "access token" that you previously issued to it.

In the case of GitHub, go to your personal settings:

![](assets/technical-setup/github-personal-settings.jpg)

Find "Applications" in the left sidebar:

![](assets/technical-setup/github-applications.jpg)

Click the "Authorized OAuth Apps" tab and then click "Revoke" next to whichever one you want to "forget":

![](assets/technical-setup/github-revoke-oauth.jpg)

Then, return to the third-party app and "Sign in with..." again to start over from scratch. In our case, click on an assignment from within Canvas again to re-start the authorization process — and this time don't forget to grant access to the organization that **_you_ created**.


### Sharing a Gitpod Snapshot

- Notes:

  - Copied from [`gitpod-snapshot.md`](https://github.com/firstdraft/appdev-chapters/blob/benp-edits/gitpod-snapshot.md){target="_blank"}

It's often helpful to share a snapshot of the state of your entire Gitpod workspace with someone else.

#### Take the snapshot

From the hamburger menu in the top-left corner of your IDE, select `Gitpod: Share Workspace Snapshot`:

![](assets/technical-setup/gitpod-snapshot-file-menu.png)

#### Copy the snapshot URL

It will take a moment to create the snapshot. Then a dialog will pop up in the bottom-right corner that will give you the URL to copy and share:

![](assets/technical-setup/gitpod-snapshot-copy-url.png)

##### The correct URL looks like this

The URL that you share should look something like this:

```
https://gitpod.io#snapshot/5a47e40d-e279-44e5-96bc-ae33cd48f151
```

Note the `#snapshot` fragment of the URL. That means you have the right one.

##### Not this

The URL should _not_ look something like this:

```
https://ac1bde40-34e8-421d-a102-6425971fb9db.ws-eu38.gitpod.io/
```

That is the URL of your own IDE, which no one else can access.

##### Or this

The URL should _not_ look something like this:

```
https://3000-ac1bde40-34e8-421d-a102-6425971fb9db.ws-eu38.gitpod.io
```

Note the `3000-` at the start. That is the URL of the live preview of your app.

#### Snapshots are completely independent

When someone clicks on the snapshot URL, they will get their own private copy of your workspace in the state that it was in when you took the snapshot.

Any changes they make to their copy will not affect your workspace. Similarly, any changes you make to your workspace won't affect their snapshot. So you can keep trying to resolve the problem on your own, or work on the next task, without interfering with their snapshot.



