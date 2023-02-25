+++
title = "Switching to Hilbish"
date = "2023-02-24T16:08:41-08:00"
author = "Daniel Xu"
authorTwitter = "" #do not include @
cover = "hilbish.png"
tags = ["shell", "linux", "terminal", "lua"]
keywords = ["", ""]
description = "Shells don't have to be POSIX compliant."
showFullContent = false
readingTime = false
hideComments = false
color = "" #color from the theme settings
+++

# Intro

Hilbish is a shell that is written in Go and scriptable in Lua. It's a relatively new face on the shell block, and I have decided to switch to it over zsh, the shell that I've been using for a long time. It supports all the basic things you would expect a shell to be able to do, including aliases, adding to the path, etc. In many respects, it fulfills what most of us use our shell for. However, if you are someone who writes advanced shell scripts in your terminal without a shebang, Hilbish isn't for you. That should mean that Hilbish is for everyone, but alas, we do not live in a perfect world. All of us sane human beings can continue believing in Lua supremacy.

# Installation

Installing Hilbish is a relatively simple task. As far as I know, Hilbish isn't on the official Arch repos nor is it on the AUR, so we'll have to build it from source. Gentoo users are probably really happy right now. First, ensure that [Go 1.17+](https://go.dev/) and [Task](https://taskfile.dev/installation/) are installed on your system, then clone Hilbish's repo.

```shell
git clone --recursive https://github.com/Rosettea/Hilbish
cd Hilbish
go get -d ./...
```
Build and install the shell by running 

```shell
task
sudo task install
```

Congratulations. You are now an ascended being.

# Usage

There are multiple ways to set Hilbish as the default shell. You can set Hilbish as the login shell by running:

```shell
chsh -s $(which hilbish)
```

However, I do *not* recommend doing this, as Hilbish is not POSIX compliant and you want your login shell to be POSIX compliant. If you do this, a couple of important environment variables might be missing. I recommend running hilbish *after* the login shell via something like `.zlogin`, which runs after the login shell when booting up your computer. For example,

```shell
exec hilbish -S -l
```

This will replace your shell with Hilbish, set the `$SHELL` variable to Hilbish and launch it as a login shell. Hilbish is, similar to Awesome, configured with an `init.lua` file located in `~/.config/hilbish`. I'll go over a few quick tips here, but I would recommend checking out Hilbish's [documentation](https://rosettea.github.io/Hilbish/docs/), as it goes way more in-depth than I ever could. 

* Path can be set like this:
```lua
hilbish.appendPath '~/.local/bin/'
```
* Aliases can be set like this:
```lua
hilbish.alias('cls', 'clear')
```

# Why I use Hilbish

I will admit, after such a long time using zsh, Hilbish took some getting used to. I found myself missing features such as tab-complete and history-based completion. For the first five minutes. Turns out, there is tab complete. It's some pretty darn good tab complete too. It knows whether to show you the results for possible files or directories or show you executables in your path. Then I accidentally pressed ctrl+r and discovered that there was history search too. Hilbish is much more fully featured out of the box than zsh is.

Truth is, you really don't need a POSIX compliant shell other than to set enviroment variables. As soon as that's done, that POSIX compliant shell can promptly frick off in favor of something else. Hilbish is just a really comfortable shell, much more so than zsh, that does everything that I need it to. That's why I use it. Also Lua. 
