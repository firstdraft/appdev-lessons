# Technical Setup: `rails grade`

- Notes:

  - manually checking work, rails grade, git commiting

### Getting automated feedback with rails grade

- Notes:

  - Copied from [`rails-grade.md`](https://github.com/firstdraft/appdev-chapters/blob/benp-edits/rails-grade.md){:target="_blank"}

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

  - Copied from [`fixing-your-organization-permissions.md`](https://github.com/firstdraft/appdev-chapters/blob/benp-edits/fixing-your-organization-permissions.md){:target="_blank"}

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

  - Copied from [`gitpod-snapshot.md`](https://github.com/firstdraft/appdev-chapters/blob/benp-edits/gitpod-snapshot.md){:target="_blank"}

It's often helpful to share a snapshot of the state of your entire Gitpod workspace with someone else.

#### Take the snapshot

From the hamburger menu in the top-left corner of your IDE, select `Gitpod: Share Workspace Snapshot`:

![](assets/technical-setup/gitpod-snapshot-file-menu.png)

#### Copy the snapshot URL

It will take a moment to create the snapshot. Then a dialog will pop up in the bottom-right corner that will give you the URL to copy and share:

![](assets/technical-setup/gitpod-snapshot-copy-url.png)

##### The correct URL looks like this

The URL that you share should look something like this:

**https\://gitpod.io#snapshot/5a47e40d-e279-44e5-96bc-ae33cd48f151**

Note the `#snapshot` fragment of the URL. That means you have the right one.

##### Not this

The URL should _not_ look something like this:

**https\://ac1bde40-34e8-421d-a102-6425971fb9db.ws-eu38.gitpod.io/**

That is the URL of your own IDE, which no one else can access.

##### Or this

The URL should _not_ look something like this:

**https\://3000-ac1bde40-34e8-421d-a102-6425971fb9db.ws-eu38.gitpod.io**

Note the `3000-` at the start. That is the URL of the live preview of your app.

#### Snapshots are completely independent

When someone clicks on the snapshot URL, they will get their own private copy of your workspace in the state that it was in when you took the snapshot.

Any changes they make to their copy will not affect your workspace. Similarly, any changes you make to your workspace won't affect their snapshot. So you can keep trying to resolve the problem on your own, or work on the next task, without interfering with their snapshot.



