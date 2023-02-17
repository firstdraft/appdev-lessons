# Rock, Paper, Scissors (RPS) -- Route, Controller, Action, View (RCAV)

We can now use HTML and CSS for designing web pages, and Ruby for writing programs. However, if we (the developers) are the only ones that can _run_ these programs (through the `ruby` interpreter), then they aren't much use. It's time to start adding an _interface_ on top of our Ruby programs so that external users can interact with them.

We already have all the tools to build our first <mark>dynamic web application</mark>. But, before we begin building, we need to understand the URL request lifecycle of _Route, Controller, Action, View (RCAV)_.

In this lesson, we will explore routing. In practice, the project we work through will make our Rock, Paper, Scissors webpage dynamic; meaning it will actually work.

## Starting Our GitPod Workspace

Before you proceed, let's get the GitPod project for this chapter

<div class="proj" markdown="1">

   **Note: these steps go for opening any GitPod project, just change the project and file names.**

   Open the GitPod `String` project on Canvas that follows this reading and start with the exercises. Follow the instructions below and complete the task in the `concat.rb` file.

   <!-- 1. LTI{Load assignment}(https://github.com/appdev-projects/ruby-project-string-1)[MV4dKHMwdAFhfRn752YW3TAY]{KBpPhe42o6wDRi35rWagKY4F}(100)[string_project] -->

   1. On Canvas, open the project assignment that follows this reading. Click on the "Load in new window" button, then click on the green button to "Create new workspace on Gitpod", which will open a new project for you to work on! **Keep this Gitpod tab open, there may be more than one exercise per chapter**. If you close the Gitpod window, you can always click the Canvas link again, but this time click "Find existing workspace in Gitpod Dashboard".

   <!-- ![](assets/string/canvas-gitpod-start-project.png) -->

   1. Open the `concat.rb` file in the editor window.

   1. Modify the file per the instructions on top.

   1. Run your Ruby file by typing `ruby ` and then the name of the file you want to run in the terminal. If we want to run `concat.rb`, we can write the command:

         ```bash
         ruby concat.rb
         ```
      
         Remember, if there are multiple files with similar names, start typing the name and then just press <kbd>Tab</kbd> on your keyboard to let the terminal complete the name. You rarely need to type full filenames out — use **tab completion**!

   1. To re-run this command, you can use the <kbd>Up ↑</kbd> and <kbd>Down ↓</kbd> arrow keys to look at the history of commands you've run in a terminal.

   1. When you think you have the required output, run `rails grade` at the terminal prompt and proceed when the test(s) passes without errors.

   If you are struggling, **try to experiment directly in the `irb` environment** by typing `irb` into the terminal and pressing enter. This will start an interactive Ruby terminal, where you can enter individual lines of Ruby to see their output. If you start `irb` then the terminal will no longer be in the `bash` environment so things like `rails grade` won't work. You will need to open a second terminal with the plus (+) icon and switch between the `irb` and `bash` terminals as needed. Alternatively type `exit` at the `irb` terminal prompt to return to the `bash` environment. If you ever want to clear the terminal output to see a fresh new line, press <kbd>Ctrl</kbd>+<kbd>K</kbd>. And if you ever close the terminal and need to re-open it, press <kbd>Ctrl</kbd>+<kbd>J</kbd>.

</div>

Enough theory. It's time to open the GitPod project so we can visualize the steps and see some results. We'll finally make our Rock, Paper, Scissors game work, by having the computer opponent randomly choose a move rather than always playing paper. We will then be able to compute outcomes based on the computer's move.

[Here](https://github.com/appdev-projects/rps-rcav){:target="_blank"} is the assignment. As usual:

  1. Start the web server by running `bin/server`.
  2. Navigate to your live application preview.
  3. As you work, remember to navigate to **/git** and *Always Be Committing (ABC)*.
  4. Organize your workspace tabs.
  5. Run `rails grade` as often as you like to see how you are doing, but make sure you *test your app manually first* to make sure it matches the target's behavior.

If you need a refresher in starting the workspace, see the [Technical Setup][Technical Setup]

The [target](https://rps-rcav.matchthetarget.com/){:target="_blank"} for this project, looks similar to what we have produced. But, the key difference is that the computer plays different moves, so the application is finally *dynamic*. 
   