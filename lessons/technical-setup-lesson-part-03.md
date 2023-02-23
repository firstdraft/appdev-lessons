# Technical Setup Part 3: /git

If you got your Canvas + Gitpod + Github trifecta setup and you can load assignments, work on projects on Gitpod, and run `rails grade` for feedback, you are in great shape! But, if you want to save all that work you are doing on Gitpod, you will need to learn about and use **git**. Read all the way to the end, your work will *not* be saved if you do not **push to Github** (see [the last section below](https://learn.firstdraft.com/lessons/30#push-to-github){:target="_blank"}).

## What Git is

[Git](https://en.wikipedia.org/wiki/Git) is an extremely powerful **version-control system** created by Linus Torvalds in 2005 for development of the Linux kernel, which is one of the largest open-source software projects in existence. It makes it possible for large numbers of contributors to work on various features, all within a single codebase (which could be comprised of hundreds or thousands of files).

Bitbucket, GitLab, and especially GitHub (all private companies) rode the rise of Git (the protocol) to become the center of the software development universe. All of these companies basically offer cloud-based storage for codebases using Git for version-control (we refer to these codebases as **repositories** or **repos**), as well as a web-based interface for collaborating on them — following, commenting, etc.

## Using /git in your projects

In this course, we're going to use one simple but effective Git-based workflow to save versions of our work. This will allow us to freely experiment with different approaches, while never having to throw away code.

In all of our Rails apps, after you start the server by running `bin/server`, you can navigate to the address **/git** in your live application. If you're using Gitpod, the URL will look like:

  **https\://[YOUR GITPOD WORKSPACE URL].gitpod.io/git**

That will open a page that looks like this:

<!-- ![](assets/technical-setup/git-clean.png) -->
![file](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1677021729/git-clean_xaw62f.png)

As soon as you make any changes to any of the code in the project, and refresh this page, the lines that you changed will appear:

<!-- ![](assets/technical-setup/git-changes.png) -->
![file](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1677021737/git-changes_yqutre.png)

On the left, you see the code as it was previously; on the right, you see the new code. Lines added are highlighted in green, lines removed are highlighted in red.

Below, there are two things you can do: **commit** your changes on the left, and switch to a new **branch** on the right. When you hear the word "commit", think "snapshot". When you hear the word "branch", think "version".

A Git commit is a snapshot of _all_ of the folders and files in your project _at a particular time_. Since our files of code are all interdependent, it doesn't make sense to save versions of individual files — we need to know the _entire_ state of the project for a version to be useful.

Each branch ("version") is a series of commits ("snapshots").

The most important thing for you to remember is simple: **commit early and commit often**. As long as you are taking snapshots of your work at various points, it will always be easy to get back to a previous state in case you want to start over and explore a different approach.

To commit, enter a title for the snapshot (required), and, optionally, a longer description:

<!-- ![](assets/technical-setup/git-commit.png) -->
![file](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1677021745/git-commit_xvfzmr.png)

After you commit, you will no longer have any pending changes:

<!-- ![](assets/technical-setup/git-changes-committed.png) -->
![file](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1677021753/git-changes-committed_ik5gza.png)

If you edit your code again, then you can make further commits.

**Fundamentally, that's all you need to worry about: just make lots of commits as you work.**

The best time to commit is right after you just got something to work, before you start on your next experiment.

Remember: **ABC**: *Always Be Committing (ABC)*.

### Jumping back in time

In the History dialog at the bottom, you can see a list of all of the commits you've made. If you want to jump back in time to one of them, copy the 7 letter code (known as the "hash" of the commit; it is a unique identifier) in front of it into the "Branch off of" field above. Pick a name for a new version, and click "Create a new branch off of...".

It will snap all of the files in the project back to that point in time, and you can now make further commits along a new path — while still retaining all of your old commits on the old path.

<!-- ![](assets/technical-setup/git-jump-back.png) -->
![file](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1677021770/git-jump-back_qwhe7v.png)

You can easily jump to any commit from any branch at any time — so feel free to experiment! Make a commit to save your current work, then jump back to a previous commit to try a different approach.

### Switch to a Different Branch

Have you gone back in time and decided your first attempt was better? Turn your attention to the "Existing Branches" panel on the right. This will list any branches your project has— `master` is the default starting branch. To switch to a different branch, click the blue double arrow button next to the name of the branch you want to switch to.

<!-- ![](assets/technical-setup/git-switch-branch.png) -->
![file](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1677021790/git-switch-branch_vxshtm.png)

If you're ever unsure of what branch you're on, the top of the page should list "On branch \_\_\_".

### Push to GitHub

Gitpod workspaces are not permanent! Even if we make git commits, if the workspace is deleted so is all of our work! This is where GitHub comes in. We can push all of the commits we've made to our repository on GitHub where it will live forever. If our Gitpod workspace gets destroyed we can just re-create another one from the latest commit on GitHub!

<aside markdown="1">
Gitpod will delete an inactive workspace after **14 days**. If you want to save the changes you've made for longer, you can "pin" a workspace in Gitpod which will prevent it from being deleted. Even better, you can push your changes to Github as explained in this section.
</aside>

<!-- Before you can push to GitHub, you need to give Gitpod access. Head over to the [Integrations under your account settings](https://gitpod.io/integrations) in Gitpod and make sure you check "public repos" and click "Update". 

![](assets/technical-setup/gitpod-integration-settings.png)
![file](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1677021803/gitpod-integration-settings_kj5kdk.png)

This should open a GitHub authorization dialogue.

**Make sure to click "Grant" next to the GitHub organization you created for class**

![](assets/technical-setup/gitpod-github-organization-permissions.png)
![file](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1677021814/gitpod-github-organization-permissions_tk39h3.png)

Now you should be all set to push your commits to GitHub! -->

Before we can push our code from our Gitpod workspace to our GitHub account (for eternal safekeeping), we need to give Gitpod permission to manage our repositories and to interact with our organization.

1. If you try clicking "Push to GitHub" and see an authentication error like this:

    ![file](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1675450072/image-1675450068951.png.png)

1. Visit the Gitpod dashboard, click your icon in the top-right corner, and select "Settings":

    ![file](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1675436202/image-1675436201460.png.png)

1. Click "Integrations" in the left sidebar, click the "..." next to "GitHub",  and select "Edit Permissions":

    ![file](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1675436351/image-1675436351144.png.png)
		
1. Make sure that **public_repo** and **repo** are checked, and then "Update Permissions" if necessary:

    ![file](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1675436485/image-1675436484581.png.png)
		
1. Next, "Manage on GitHub":

    ![file](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1675436748/image-1675436747740.png.png)
		
1. Ensure that your organization has permission. If not, click "Grant" next to its name:

    ![file](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1675436779/image-1675436779288.png.png)

1. Finally, try clicking "Push to GitHub" again:

    ![file](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1675450219/image-1675450216406.png.png)
		
		
Now, you should get into the habit of pushing your code to GitHub very often. If you do, then you're certain never to lose your work, among many other benefits of using GitHub to store your code.

#### Quiz Question

- Were you able to follow the steps above and push to GitHub successfully?
- Yes
    - Great! 
- No
    - Please find an instructor for help. Pushing to GitHub is important! We need to get it sorted ASAP.
{: .choose_best #completion points="1" answer="1" }