# Technical Setup: Gitpod Projects

The assignments in this course will mostly follow the workflow outlined below. Many of these steps only need to be done the first time you set up the Canvas + Gitpod + Github trifecta. **If you are getting errors with the steps outlined below, carefully follow the instructions [here] TODO: link to part 05 fixing permissions**

## First time set up

Once you do these steps once, you can jump right ahead to **TODO: link to lower part of lesson** if you need a referesher in the daily workflow of working on a Gitpod assignment and gettng feedback.

### Join GitHub

If you haven't already, [sign up for a free GitHub account](https://github.com/join) (or sign in to yours if you already have one):

<!-- ![](assets/technical-setup/join-github.png) -->
![file](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1677020920/join-github_czxbwn.png)

In this example screenshot, I chose a username of `demolearner1` — remember yours. Also, don't forget to check your email and verify the address you entered.

For now, think of GitHub like Dropbox-for-programmers; it's where we're going to store all of our code.

### Create GitHub organization

To keep things organized, we're going to create a separate GitHub organization account for you to store your AppDev projects under (to keep them separate from the personal projects that you'll hopefully be building soon!).

Click the `+` on the right side of the navbar and select "New organization":

<!-- ![](assets/technical-setup/new-organization.png) -->
![file](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1677020945/new-organization_f3zevo.png)

Choose any name for the organization; most students choose `[YOUR USERNAME]-appdev`. In this example screenshot, I chose `demolearner1-appdev`:

<!-- ![](assets/technical-setup/org-name.png) -->
![file](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1677020982/org-name_y98heg.png)

You can "Skip" or "Finish" the rest of the screens:

<!-- ![](assets/technical-setup/finish-org.png) -->
![file](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1677021002/finish-org_wpmmlc.png)

### Starting a Gitpod Assignment

Typically, we will assign you a project in Canvas. The assignment will include a button that says "Load assignment in a new window". When you click on that button, it will create a fork (i.e. a copy) of the repository (i.e. the folder of code) on your own GitHub account.

You will then create a Gitpod workspace based on _your_ fork, so that you can save the work that you do back to your own GitHub account. A button to create your Gitpod workspace will appear within the assignment, so usually all you need to do is click on it after clicking "Load assignment in a new window". And then you can get right to work, with the exact right version of all of the project's dependencies ready to go!

That's the power of Gitpod.

**TODO:** link next git chapter to show how to save work

<aside markdown="1">
Gitpod will delete an inactive workspace after **14 days**. If you want to save the changes you've made for longer, you can "pin" a workspace in Gitpod which will prevent it from being deleted. Even better, you can [push your changes to Github]\(**TODO:** lessons link for: https://chapters.firstdraft.com/chapters/839#push-to-github).
</aside>


#### Login to Canvas

Open up the Assignments tab and make sure they're sorted by type.

<!-- ![](assets/technical-setup/login-canvas.png) -->
![file](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1677021025/login-canvas_pvxmxw.png)

Scroll down to the assignment you want to start and click the link that says 'Load [your assignment name] in a new window' (the name of the project will vary).

<!-- ![](assets/technical-setup/load-assignment.png) -->
![file](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1677021039/load-assignment_gcto1x.png)

**_Before_ you click "Authorize", make sure to click the "Grant" button next to the organization that you created earlier.** Only then, click authorize to allow the firstdraft Grades application to access your account. 

<!-- ![](assets/technical-setup/authorize-first-draft.png) -->
![file](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1677021048/authorize-first-draft_towhmr.png)

Select the name of your GitHub **organization** and submit the form.

<!-- ![](assets/technical-setup/add-github-org-name.png) -->
![file](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1677021058/add-github-org-name_lyvxvd.png)

The next screen will ask you to accept an invitation to a GitHub team. You can click the link on that screen to accept, or you'll have an invitation in your email inbox as well.

Once you've joined, you should see feedback that you're now a member of appdev-projects:

<!-- ![](assets/technical-setup/github-joined-org-feedback.png) -->
![file](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1677021072/github-joined-org-feedback_byfx9u.png)


## Daily workflow

The stuff above about setting up your organization and permissions was just a one-time thing. From now on, you'll just head to Canvas and click "Load assignment in a new tab". You should see something like the following (the name of the project will vary):

<!-- ![](assets/technical-setup/grade-setup-instructions.png) -->
![file](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1677021088/grade-setup-instructions_jo0tzw.png)

We will automatically make a copy (a "fork", in GitHub parlance) of the repository under your new GitHub organization. Then, you can choose to either "Create new workspace in Gitpod" or head to your "Gitpod Dashboard" to view existing workspaces.

**If you are getting errors with this process, carefully follow the instructions [here] TODO: link to part 05 fixing permissions**

### Working on a Gitpod project

<!-- **TODO: short video for this whole section** -->

The general steps for working on _any_ Gitpod project for this course are:

1. Start the web server by running `bin/server` at the terminal. <!-- **TODO: section on terminal environment and commands** -->
2. Navigate to your live application preview.
3. As you work, remember to navigate to **/git** and *Always Be Committing (ABC)*. **TODO: link to git sections**
4. Organize your workspace tabs.
5. Run `rails grade` as often as you like to see how you are doing, but make sure you *test your app manually first* to make sure it matches the target's behavior. **TODO: link to section below**

If some of those steps seem mysterious at the moment, read on! All will be explained shortly. You will get very comfortable with the steps while working on the several projects for the course.

Remember to keep the Gitpod and live application browser tabs open as you work. If you close the Gitpod workspace, you can always click the Canvas link again, but this time click "Find existing workspace in Gitpod Dashboard".

### Getting automated feedback with `rails grade`

**If you are getting errors with the below process, carefully follow the instructions [here] TODO: link to part 05 fixing permissions**

Once you're in the workspace on Gitpod, after the `bin/setup` script is done running, start working on the project to do whatever the instructions tell you. **When you're ready for feedback**, try a new command at a new terminal prompt (i.e., not in the terminal running the server that you previously ran `bin/server` in):

```
rails grade
```

You'll be asked for your access token; **copy-paste it carefully from the grades.firstdraft.com page that you loaded from Canvas**.

<!-- ![](assets/technical-setup/gitpod-enter-token.png) -->
![file](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1677021108/gitpod-enter-token_rxuau9.png)

You should see output that looks like:

<!-- ![](assets/technical-setup/gitpod-rails-grade.png) -->
![file](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1677021116/gitpod-rails-grade_cw3zpg.png)

Copy-paste the Results URL into a new tab, or click on it (but make sure it isn't truncated).

<!-- ![](assets/technical-setup/gitpod-rails-grade-open.png) -->
![file](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1677021124/gitpod-rails-grade-open_x94mpt.png)

<!-- ![](assets/technical-setup/rails-grade-results.png) -->
![file](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1677021139/rails-grade-results_jhfzhn.png)

**(Some projects aren't graded; in that case there may only be one dummy test listed.)**

You can click on one of the tests to get more feedback on what might have gone wrong:

<!-- ![](assets/technical-setup/rails-grade-results-details.png) -->
![file](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1677021147/rails-grade-results-details_v9q2o4.png)

In this case, the test expected to find an element with a class of `word_count` that contains the number 10, but instead it only found the content "Replace this string with your answer". 

You can click the "Examine Test" button to read the actual Ruby of the automated test; it's surprisingly readable. Ruby's testing libraries use method names that are supposed to make tests readable even for non-technical managers and clients. You can see specifically what flow is being tested and what inputs are being used and what the expected output is, and try to reproduce the issue in your own app manually using the same inputs.

You can run `rails grade` in your terminal as many times as you want, and you will get a new updated build report each time. It will only report your highest score back to Canvas.

**Remember that your first job is always to make your app work as described and test it manually yourself. You should not rely exclusively on the automated tests; they are a terrible way to debug.**

### Sharing a Gitpod snapshot

It's often helpful to share a snapshot of the state of your entire Gitpod workspace with someone else.

#### Take the snapshot

From the hamburger menu in the top-left corner of your IDE, select `Gitpod: Share Workspace Snapshot`:

<!-- ![](assets/technical-setup/gitpod-snapshot-file-menu.png) -->
![file](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1677021161/gitpod-snapshot-file-menu_ih8ihp.png)

#### Copy the snapshot URL

It will take a moment to create the snapshot. Then a dialog will pop up in the bottom-right corner that will give you the URL to copy and share:

<!-- ![](assets/technical-setup/gitpod-snapshot-copy-url.png) -->
![file](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1677021172/gitpod-snapshot-copy-url_zdlmmn.png)

**The URL should look like this:**

  - **https\://gitpod.io#snapshot/5a47e40d-e279-44e5-96bc-ae33cd48f151**

Note the `#snapshot` fragment of the URL. That means you have the right one.

**The URL should NOT look like these:**

  - **https\://ac1bde40-34e8-421d-a102-6425971fb9db.ws-eu38.gitpod.io/**

    That is the URL of your own IDE, which no one else can access.

  - **https\://3000-ac1bde40-34e8-421d-a102-6425971fb9db.ws-eu38.gitpod.io**

    Note the `3000-` at the start. That is the URL of the live preview of your app.

#### Snapshots are completely independent

When someone clicks on the snapshot URL, they will get their own private copy of your workspace in the state that it was in when you took the snapshot.

Any changes they make to their copy will not affect your workspace. Similarly, any changes you make to your workspace won't affect their snapshot. So you can keep trying to resolve the problem on your own, or work on the next task, without interfering with their snapshot.



