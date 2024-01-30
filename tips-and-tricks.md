# Gitpod keyboard shortcuts and other productivity tips

## Important Terminal keystrokes to know

### Jump to beginning of line

You can't use your mouse at the command line, so it's important to know how to move around quickly so you're not restricted to just using your arrows. Jump back to the beginning of the line with <kbd>Ctrl</kbd> + <kbd>A</kbd>:

![](/assets/back-to-beginning.gif)

### Jump to end of line

Mac OS, Windows: <kbd>Ctrl</kbd> + <kbd>E</kbd>

![](/assets/back-to-end.gif)

### Up and down arrows to scroll through your history

Use your up and down arrows to scroll through your command history so that you don't have to re-type your commands over and over.

![](/assets/previous-terminal-command.gif)

### Clear Terminal

Mac OS: <kbd>Command</kbd> + <kbd>K</kbd>

Windows: Disabled by default[^windows-clear]. See below instructions to enable it — we strongly recommend that you do this.

![](/assets/clear_terminal.gif)


[^windows-clear]: A recent Gitpod update removed this keyboard shortcut for Windows, so you'll need to configure it yourself.

From the menu open Preferences and select Keyboard shortcuts.

![](/assets/gitpod-keyboard-shortcuts.png)

Then search for "terminal clear" in the search bar and click the plus icon to the left of it.

![](/assets/gitpod-clear-terminal.png)

Finally, type <kbd>ctrl</kbd> + <kbd>k</kbd> and <kbd>Enter</kbd> to confirm.

![](/assets/gitpod-ctrl-k.png)

### Interrupt command

If something goes wrong with a terminal program (i.e. you made a typo, a program gets stuck in an infinite loop, etc), you can generally interrupt it with <kbd>Ctrl</kbd> + <kbd>C</kbd>:

![](/assets/ctrl-c-to-quit.gif)

### Q to exit

When the output of a terminal command is too tall for a terminal tab to display at once, it paginates. Press <kbd>Space</kbd> to step through it one page at a time, or <kbd>Q</kbd> to quit and get back to the terminal prompt so that you can execute your next command.

Mac OS, Windows: <kbd>Q</kbd>

![](/assets/q-to-exit.gif)

## Editor keyboard shortcuts

### Command Palette

The most important thing to memorize is how to open the **Command Palette**, which will allow you to fuzzy search within for all other commands. If the command has a keyboard shortcut mapped to it, the shortcut will be displayed to the right. This is the best way to learn the keyboard shortcuts for the commands that you use most frequently.

Mac OS: <kbd>Command</kbd> + <kbd>Shift</kbd> + <kbd>P</kbd>

Windows: <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>P</kbd>

![](/assets/gitpod-command-palette.gif)

### Quick open file

To quickly jump to a file:

Mac OS: <kbd>Command</kbd> + <kbd>P</kbd>

Windows: <kbd>Ctrl</kbd> + <kbd>P</kbd>

And then fuzzily search for its name. For example, you could type "phco" to get to **ph**otos_**co**ntroller.rb and the list would quickly narrow to bring that file to the top of the list.

![](/assets/open_file.gif)

### Toggle Code Comment

To quickly comment a line of code, put your cursor on that line and then:

Mac OS: <kbd>Command</kbd> + <kbd>/</kbd>

Windows: <kbd>Ctrl</kbd> + <kbd>/</kbd>

You can also highlight multiple lines of code and comment/uncomment all of them at once.

![](/assets/toggle-comment.gif)

### Find (and replace)

Mac OS: <kbd>Command</kbd> + <kbd>F</kbd>

Windows: <kbd>Ctrl</kbd> + <kbd>F</kbd>

![](/assets/find_and_replace.gif)

### Find Next Selection

Mac OS: <kbd>Command</kbd> + <kbd>D</kbd>

Windows: <kbd>Ctrl</kbd> + <kbd>D</kbd>

![](/assets/select_next.gif)

If you go too far by mistake, you can step backwards with <kbd>Command</kbd> + <kbd>U</kbd> or <kbd>Ctrl</kbd> + <kbd>U</kbd>.

### Move line

Mac OS: <kbd>Option</kbd> + <kbd>&#11015;</kbd>

Windows: <kbd>Alt</kbd> + <kbd>&#11015;</kbd>

![](/assets/move_line.gif)

### Duplicate line

Mac OS: <kbd>Shift</kbd> + <kbd>Option</kbd> + <kbd>&#11015;</kbd>

Windows: <kbd>Shift</kbd> + <kbd>Alt</kbd> + <kbd>&#11015;</kbd>

![](/assets/duplicate_line.gif)

### Add/Remove Tab spaces for multiple lines

Mac OS: (<kbd>Shift</kbd>) + <kbd>Tab</kbd>

Windows: (<kbd>Shift</kbd>) + <kbd>Tab</kbd>

![](/assets/tab-spacing.gif)

### Add More Cursors

Mac OS: <kbd>Option</kbd> + Click

Windows: <kbd>Alt</kbd> + Click

![](/assets/multiple-cursors.gif)

### Embedded Ruby (ERB) Tag Toggle

Mac OS, Windows: <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>`</kbd>

![](/assets/ERB-shortcut.gif)

### Toggle Terminal Panel

Mac OS: <kbd>Command</kbd> + <kbd>J</kbd>

Windows: <kbd>Ctrl</kbd> + <kbd>J</kbd>

![](/assets/toggle_terminal_view.gif)

### Open New Terminal

Mac OS: <kbd>Ctrl</kbd> + <kbd>~</kbd> (i.e. <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>`</kbd>)

Windows: <kbd>Ctrl</kbd> + <kbd>~</kbd> (i.e. <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>`</kbd>)

![](/assets/new_terminal.gif)


