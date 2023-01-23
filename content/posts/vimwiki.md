---
title: "Vimwiki"
date: 2023-01-22T23:43:35-08:00
draft: false
category: personal-knowledge
---
# Why Vimwiki is the Best Notetaking Sofware

## What is Vimwiki?

It's a bit difficult to explain Vimwiki, but at its core, Vimwiki is a notetaking plugin for Vim that allows you to make your own personal wiki. It's really easy to organize notes and create links between them. You can do so many things with Vimwiki, and Vimwiki has all but replaced Emacs Org Mode for me, as it is now much easier to organize my notes with Vimwiki than just shove all of my Org files in a directory in my home folder.
=> https://github.com/vimwiki/vimwiki Vimwiki Github

## Installation

Vimwiki was made for Vim, and as far as I know, it does not officially support Neovim yet. You can still use it with Neovim, though. To install Vimwiki on Neovim, simply plug "vimwiki/vimwiki" into your package manager. For example, with Packer, it looks something like this:

```
use {'vimwiki/vimwiki'}
```

However, this installs Vimwiki with its default syntax, which is this weird version of Markdown that I really don't like. So, I put this in my `plugins.lua`:

```
  use {
      'vimwiki/vimwiki',
      config = function()
          vim.g.vimwiki_list = {
              {
                  path = '/home/$USER/Documents/vimwiki',
                  syntax = 'markdown',
                  ext = '.md',
              }
          }
      end
  }
```

This changes the syntax for files created using Vimwiki to Markdown syntax, as well as changing the file extensions to `.md`. It also changes your Vimwiki's location from the default ~/vimwiki to a folder in your Documents directory named Vimwiki. Much better. To finish the installation, restart Neovim.

## Usage

### Creating Index.md and a new note.

In order to open your `index.md` file, which is sort of like the home page for your Vimwiki, the default keybinding is `<leader> ww`. This will create an `index.wiki` file in the specified path, which in our case is `Documents/wimwiki`. This document will be blank since you haven't put anything in it yet, so lets change that. In order to create a new Vimwiki page, simply type the title of the page, highlight the title, go into normal mode, and press the return key. That converts the selected text into a link and creates a new document with the specified title.

```
[Quick Notes](Quick Notes)
```

Press enter again to jump to the newly created document. At this point, you can just write whatever you want in markdown and :w to save.

### Todo Lists

Todo lists are incredibly convenient to manage in Vimwiki. Just create a new note named `Todo`. To create a todo list in your newly created document, put your todo in this syntax.

```
* [ ] Write a blog post about Vimwiki.
```

Now every time you press return, a new todo will automatically be created for you. I suggest following the rules for a `todo.txt` file just because that's what I do, but organize your todos however you like. In order to mark a todo as done, simply hit `ctrl-space` while in normal mode with your cursor on the todo entry.

These are the only two features of Vimwiki that I actually use, so those will be the only ones I'm covering in this post, but there is another really cool feature in Vimwiki called diary. Brodie Robertson has a superb video covering this feature on his
=> https://www.youtube.com/watch?v=FsX3SpHiuYw Youtube channel

## Final Thoughts

Vimwiki is a superb note taking sofware, and I'm basically using it full-time now for everything from school to todo to blog posts to jotting down quick notes. In fact, I'm writing this blog post in it right now. It's just so convenient for me, and I suggest you try it out as well.
