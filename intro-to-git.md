# Intro to Git

## Setup

### Sign up for a GitHub account

If you don't already have one, [sign up for a GitHub account](https://github.com/join){:target="_blank"}. There are a bunch of [student benefits](https://education.github.com/pack){:target="_blank"} that you can get through GitHub, so you might want to use a school-issued email address if you have one.

![](/assets/intro-to-git-01.png)

### Create a repository

[Create a new repository](https://github.com/new){:target="_blank"}, selecting the "Add a README file" option.

![](/assets/intro-to-git-02.png)

### Sign up for a Gitpod account

At this stage, you would download, or "clone", the repository to your own computer to start working with it. To save time initially, we're going to use a cloud-based development environment instead of our own computers.

Head to [Gitpod](https://www.gitpod.io/github-student-developer-pack){:target="_blank"} and sign up using your GitHub account. They have a student discount through the GitHub Student Developer Pack which gets you extra benefits, but you can also just sign up for the free tier.

![](/assets/intro-to-git-03.png)

### Create a workspace based on your repo

Once you have a Gitpod account, you're ready to clone the code in your repository (right now, just the README file and nothing else) and start working with it in a "workspace" (what Gitpod calls the cloud-based development environments they provide us).

Gitpod makes it really easy to clone the code in any GitHub repo: get the URL of the repo, and paste it after `https://gitpod.io/#`. For example, my repo's URL is:

```
https://github.com/demostudent15/playing-around
```

So to create a workspace and download the code in that repo, I need to visit[^gitpod_extension]:

[^gitpod_extension]: There's also a handy browser extension you can install that makes creating workspaces a one-click experience. [Read more here.](https://www.gitpod.io/docs/getting-started#start-your-first-workspace){:target="_blank"}

```
https://gitpod.io/#https://github.com/demostudent15/playing-around
```

Create a workspace based on the repository you created above now.

![](/assets/intro-to-git-04.png)

### Add some files

The IDE (Integrated Development Environment) that you find yourself in is full-fledged [Microsoft VSCode](https://code.visualstudio.com/){:target="_blank"}, my text editor of choice even when I'm writing code on my own computer; which is pretty darn amazing to have running right inside our browser. At the left is a file explorer, at the bottom is a terminal window with a command-line interface to the computer Gitpod is giving us, and at the top-right is the text editing pane.

Find the three dots at the top of the file explorer and create a few files. 

![](/assets/intro-to-git-05.png)

I made five:

 - `mon.md`
 - `tue.md`
 - `wed.md`
 - `thu.md`
 - `fri.md`

### Learn Markdown

The `.md` extension is for Markdown, an extremely handy formatting language. It's 1/10th as cumbersome to type as HTML, 1/100th as cumbersome to type as LaTeX, but for the vast majority of your writing you can achieve what you need to with Markdown.

Most importantly for us, GitHub supports Markdown in comments (which we'll be writing a lot if we're on a good team), so we should get comfortable with it. [Here is a Markdown cheat sheet](https://gist.github.com/raghubetina/a1b6e89e24a8c3acae6f0b63a1fd3323){:target="_blank"} with examples. It'll take you five minutes to read through it, and it covers 99% of what you'll use day-to-day.

You can try out your Markdown skills by writing a task list in `mon.md` of some things you need to do on Monday. Click the icon in the top-right corner of the editing pane to preview the rendered Markdown:

![](/assets/intro-to-git-06.png)

Add at least a heading to each file.

### Turn on Autosave

To save a lot of headache, turn on Autosave from the File menu:

![](/assets/intro-to-git-07.png)

## Command-line Git basics

Finally, let's get started learning how to version control with Git. Git is a very powerful tool with a _lot_ of commands. Here is the small subset of commands that I use a million times a day.

### Initialize a repo

For the record, in case you were starting a Git repository in an existing folder on your own computer (instead of with a README on GitHub the way we did it), to initialize a repository in a you would `cd` in to the folder and then:
 
```
git init
```

Then you would select the "Create a blank repository" option in GitHub and use the commands they give you to push your code to them.

### Create a commit

To take a snapshot of your work (all of the files and subfolders)[^staging_files], use the following two commands from the root folder of the repository:

```
git add -A
git commit -m "Created task list for each day"
```

[^staging_files]: `git add -A` adds _all_ of the files and subfolders in the project to the commit. You don't have to do that — if you only want to add the changes from one or two files, you can "stage" them one at a time:

    ```
    git add path/to/file1
    git add location/of/file2
    git commit -m "My surgical commit"
    ```

### Check your status often

To see the current status of the repository (are there any changed files since the last commit? etc):

```
git status
```
 
### See what's changed with diff

To see the line-by-line changes since the last commit:

```
git diff
```

Add a few tasks in a few different files and then try `git diff`. If the output is very long, use the space bar to page through results; or press <kbd>q</kbd> to quit and get back to the command prompt.

### Create a new branch

To start a new version, or **branch**:

```
git checkout -b week-of-2021-08-09
```

In each file, use [strikethrough](https://gist.github.com/raghubetina/a1b6e89e24a8c3acae6f0b63a1fd3323#strikethrough){:target="_blank"} to cross off some finished tasks, and add some new tasks that you predict for the following week. Then commit the changes.

### Switch to a different branch

To list all branches:

```
git branch
```

To switch to another existing branch:

```
git checkout branch-name
```

A convenient nickname for "the branch I was just on" is `-`, so an easy way to toggle back and forth between two branches is:

```
git checkout -
git checkout -
git checkout -
```

Notice how _all_ of the files snap back and forth as you are toggling branches. Neat!

When we're writing code, it's good to branch early and often. There's no cost to it and there's lots of benefits to it. In particular, it's good to start a new branch for each _task_ or _feature_. Or just a different approach to the same task, to make it easy to get back to a clean state if you want to start over.

### Always Be Committing

Try to make your commit messages somewhat descriptive of what you did since the last snapshot, but it's more important that you just **make lots of commits**. So if you must just say `git commit -m "WIP"` (for "work in progress"), that's fine; we can clean it up later.

Our golden rule: **A**lways **B**e **C**ommitting. As long as you do that, everything will be okay; we can recover from anything with Git as long as you commit early and often. You cannot _over_ commit but you can most certainly _under_ commit.

### Stash changes

Sometimes, if you have made edits to files that you haven't committed yet, it won't let you switch to another branch. Which is good; you have to make a decision about those changes first — do you want to save them or not? Your options:

  - Make a commit first, and then you can switch to the other branch.
  - If you don't want to pollute your current branch, you can make a new branch, commit the changes, and then switch to the other branch.
  - You can quickly "stash" the changes with `git add -A; git stash`. This puts the changes into a randomly named branch that will eventually be deleted after a few weeks, but until then you can get the changes back if you want them. This is the equivalent of the above, but saves you the trouble of having to think of a name for the new branch.
  
  I usually just think of `git add -A; git stash` as a convenient way to discard all the changes since my most recent commit, so that I can start afresh; but, there _is_ a way to get those changes back if I want them (this only happens about once a year).
 
### See the git log

To see the history of your current branch:

```
git log
```

You will see the author, date, and title of each commit preceded by a long sequence of letters and numbers known as the "SHA-1 hash" of the commit. This is a unique fingerprint of the snapshot.

To see a graph of all your branches at once, try:

```
git log --oneline --decorate --graph --all -30
```

### Jump back to a previous commit

To jump back to a prior commit:

```
git checkout [SHA of commit you want to go back to]
```

Find the SHA by looking at the output if `git log`. Just the first 7 or so digits of the SHA are enough; you don't need the whole thing.

If you jump to a commit like this, you'll be in a "detached" state — i.e., not on any branch. This is okay for browsing, but it's best not to make any changes.

If you want to start a new branch from this point, though, that's perfectly fine — I do that all the time when I decide I want to try a new approach. Just `git checkout -b new-branch-name` and then continue making commits as usual.

### Push to GitHub

When you're ready to send the work you've done on a branch back to GitHub.com:

```
git push
```

The very first time you `push` to a branch, it may ask you to do something like:
        
```
git push --set-upstream origin your-branch-name
```

The very first time you `push` to GitHub from Gitpod, it will ask you to give it permission to do so. Go ahead and do so from [Integrations under your account settings](https://gitpod.io/integrations):

![](/assets/intro-to-git-08.png)

### Pull from GitHub

To retrieve the freshest version of the branch you're on from GitHub.com, in case there have been any updates (e.g. from collaborators):

```
git pull
```

### Start on a new task

When you're ready to start on a new task, the best practice is to first switch back to the `main` branch, get the freshest version, and then to start a new branch from there:

```
git checkout main
git pull
git checkout -b my-next-task
```

### Don't commit to main

It's almost never a good idea to make commits directly to the `main` branch. Make a new branch, make commits to it as you're working, push your changes to GitHub, open a Pull Request, review your changes there in the Files Changed tab and make sure everything looks good.

## Merging branches

When you're ready to bring the changes from one branch (usually from one of your experimental branches, e.g. `your-name-first-branch`) into another branch (usually into the `main` branch), we have a couple of options:

 1. Fundamentally, we use Git's `merge` command at the command-line.
 1. In the early days, I recommend pushing your branch to GitHub and using GitHub's interface for merging.

### Use GitHub's interface to merge

To merge changes from e.g. `your-name-first-branch` into `main` remotely using GitHub's web UI:

 1. Push your branch to GitHub:
 
    ```
git checkout your-name-first-branch
git push
    ```
    
 1. [Create a Pull Request](https://docs.github.com/en/github/collaborating-with-issues-and-pull-requests/creating-a-pull-request){:target="_blank}.
 2. If there have been any commits on `main` since the time you branched off it, and if any of those commits have modified the same lines of code that your commits have modified, you will have to [reconcile how you want those conflicts to be handled](https://docs.github.com/en/github/collaborating-with-issues-and-pull-requests/resolving-a-merge-conflict-on-github){:target="_blank}.
 3. [Merge the PR](https://docs.github.com/en/github/collaborating-with-issues-and-pull-requests/merging-a-pull-request){:target="_blank}. You're given a few strategies to choose from on how to do so; choose [Squash and merge](https://docs.github.com/en/github/collaborating-with-issues-and-pull-requests/about-pull-request-merges#squash-and-merge-your-pull-request-commits){:target="_blank}. This will combine all of your work-in-progress commits into just one commit; now's your chance to craft [a wonderful commit message](https://chris.beams.io/posts/git-commit/){:target="_blank} to [communicate the WHY of your changes](https://dhwthompson.com/2019/my-favourite-git-commit){:target="_blank} (the WHAT is told by the diff).
 4. Switch back to `main` on your machine and fetch the merged version:
 
    ```
git checkout main
git pull
    ```

### git merge command

To merge changes from e.g. `your-name-first-branch` into `main` locally using `git merge`:

 1. First switch to `main` and make sure it is up to date:
 
    ```
git checkout main
git pull
    ```
    
 1. Switch back to your feature branch and "rebase interactively" onto `main`. This means, essentially, sync up the feature branch with any changes that may have occurred on `main` since they time you created the branch:
 
    ```
git checkout your-name-first-branch
git rebase main -i
    ```
    
 1. A text editor will pop up with a list of all of the commits you made along the way on your feature branch. Replace `pick` for all but the first one of them with `s` (for `squash`). Save and close the file.
 2. Another text editor will open where you can craft [a wonderful commit message](https://chris.beams.io/posts/git-commit/){:target="_blank} to [communicate the WHY of your changes](https://dhwthompson.com/2019/my-favourite-git-commit){:target="_blank} (the WHAT is told by the diff).
 3. Now that all your messy work-in-progress commits have been ironed out, we can merge:
 
    ```
git checkout main
git merge your-name-first-branch
    ```
 
 1. That's it — verify with `git log`. It's as if you made one, beautiful commit directly to `main`.
 2. Now you can `git push` your `main` to GitHub to share your work with your team and make it an official, unchangeable part of the history.
 3. `git checkout -b` a new branch for your next task, rinse, and repeat.

You may hear about many other commands available in Git (`cherry-pick`, `reflog`, `bisect`), and they can indeed come in handy in rare cases, but the above workflow is extremely powerful and are the commands that I use 99.99% of the time. They will take you far, once you get the hang of them.

## Graphical Git interfaces

The above command-line Git commands are good to know, because you will often find yourself using computers (like a university computing cluster) that only have command-line interfaces. But, on your own computer, you might be interested in a visual interface to Git instead; the command-line commands are, admittedly, horrible. And it's really nice to _see_ branches and commits spread out in a nice graph, and be able to switch between them and merge with just a click.

There are a lot of Git GUIs, and you should explore, but I like [GitKraken](https://www.gitkraken.com/){:target="_blank}. They also have good [learning resources](https://www.gitkraken.com/learn/git/tutorials){:target="_blank}.

## Learning more advanced Git

After you get the hangs of the basics, here are some resources to learn more about Git:

 - [Learn Git Branching game](https://learngitbranching.js.org/){:target="_blank}
 - [Oh Shit, Git!?!](https://ohshitgit.com/){:target="_blank}
 - [How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/){:target="_blank}
 - [My favorite Git Commit](http://my%20favourite%20git%20commit/){:target="_blank}
 - [Mastering Git](https://thoughtbot.com/upcase/mastering-git){:target="_blank}
 - Drop us a line! We love answering questions.

This guide is a work in progress!

---
