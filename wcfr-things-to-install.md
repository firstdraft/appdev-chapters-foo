# [WCfR] Things to install

Here are a few tools that we recommend installing so that you can hit the ground running:

## Windows users: Install Windows Subsystem for Linux

Most developers use Linux or MacOS computers (which share Unix DNA); and most applications are deployed to Linux servers. So most of the software we use is optimized for and battle-tested on *nix. Windows users can often struggle to get things running, or find answers online when things don't work.

Fortunately, Microsoft recently incorporated a straightforward way to run full-fledged Linux within Windows: Windows Subsystem for Linux, or WSL. I recommend installing it if you're on Windows, and using it for most of your software development (as opposed to DOS/Windows Command Prompt).

[Follow the official guide to install WSL and update to WSL2.](https://docs.microsoft.com/en-us/windows/wsl/install-win10){:target="_blank"} I recommend the latest Ubuntu when asked to choose a Linux distribution.

## Docker

Docker is a tool that lets us wrap up and distribute computing environments, including all of the packages that a build process depends on. This is a boon for reproducibility.

[Install Docker.](https://docs.docker.com/get-docker/){:target="_blank"}

## VSCode

VSCode is a great general-purpose text editor. We'll also use it to ease SSHing into remote servers, using Docker containers, and more.

 - [Download and install VSCode.](https://code.visualstudio.com/download){:target="_blank"}
 - Install the [Remote Development extension pack](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.vscode-remote-extensionpack){:target="_blank"}
    - Windows users: Note that you must [install a supported SSH client](https://code.visualstudio.com/docs/remote/troubleshooting#_installing-a-supported-ssh-client){:target="_blank"}.
 - Optionally:
    - Explore [popular extensions](https://www.educative.io/blog/top-vscode-extensions){:target="_blank"} and experiment with ones that sound interesting.
    - There are extensions that provide extra features for nearly any language, [like this one for R.](https://marketplace.visualstudio.com/items?itemName=Ikuyadeu.r){:target="_blank"}
    - There are [many color schemes](https://www.spec-india.com/blog/vscode-themes){:target="_blank"} you can install.
    - I like to customize my fonts for programming for better legibility; [Iosevka Curly Slab](https://typeof.net/Iosevka/){:target="_blank"} and [Input Mono](https://input.djr.com/download/){:target="_blank"} are two favorites. Or you can explore a _whole bunch_ more side-by-side at [programmingfonts.org](https://www.programmingfonts.org/){:target="_blank"}.

## GitKraken

GitKraken is my preferred GUI for Git. [Download and install](https://support.gitkraken.com/how-to-install/){:target="_blank"} the free version (you don't need a license).

GitKraken [offers good video tutorials on Git, GitHub, and GitKraken](https://www.gitkraken.com/learn/git/tutorials){:target="_blank"}. Check them out.

## Python with Conda

[Install Anaconda](https://docs.continuum.io/anaconda/install/){:target="_blank"} if you don't already have a Python version manager that you like.
