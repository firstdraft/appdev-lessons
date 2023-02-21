# Technical Setup: Gitpod Tips and Tricks

<aside markdown="1">
Gitpod will delete an inactive workspace after **14 days**. If you want to save the changes you've made for longer, you can "pin" a workspace in Gitpod which will prevent it from being deleted. Even better, you can [push your changes to Github]\(**TODO:** lessons link for: https://chapters.firstdraft.com/chapters/839#push-to-github).
</aside>

### Forcing Chrome to "Hard" Refresh

- Notes: 

  - Copied from [`hard-reload.md`](https://github.com/firstdraft/appdev-chapters/blob/benp-edits/hard-reload.md){:target="_blank"}

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

  - Copied from [`tips-and-tricks.md`](https://github.com/firstdraft/appdev-chapters/blob/benp-edits/tips-and-tricks.md){:target="_blank"}

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

Windows: Disabled by default. A recent Gitpod update removed this keyboard shortcut for Windows, so you'll need to configure it yourself.

![](assets/technical-setup/clear_terminal.gif)


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