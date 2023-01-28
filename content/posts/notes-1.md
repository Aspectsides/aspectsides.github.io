---
title: "Setting up Neovim for Editing LaTeX"
date: 2023-01-28T12:45:41-08:00
draft: false
---

This is the first article in a three part series in which I discuss how I write math notes with LaTeX and Neovim.

## Why I Started Using LaTeX

  One thing I've always recognized about myself is that I have terrible handwriting. Problem is, I'm a math major. I kinda need to be able to read my lecture notes later so I don't fail the class. That's when I discovered [this](https://castel.dev/post/lecture-notes-1/) blog post by Gilles Castel. It introduced me to the magic of Neovim combined with LaTeX. It took me a while to learn, but after becoming proficient in LaTeX i find that I can take much more readable math notes as well as being able to type them up faster than all my clasmates. They think I'm a wizard.
  
## Setting up Neovim

  Here is what my screen looks like when I'm writing LaTeX notes: 
  
  ![Latex](/static/latex1.png)
  
  The window on the left is Neovim configured with a few plugins that enhance the LaTeX experience. The window on the left is Zathura, my PDF reader that updates whenever I recompile my LaTeX file by saving it.
  
  I use my own Neovim configuration written in Lua. You can get it over on my [Github](https://github.com/aspectsides/archfiles). Configuring Neovim from scratch is very time consuming, so if you just want to get started with LaTeX you can steal my config.
  
  ### Plugins 
  
  There are a few choice plugins that I find greatly enhances my efficiency whenever I'm typing LaTeX. The first is [vimtex](https://github.com/lervag/vimtex). You can install this plugin using your preferred package manager. I use [packer](https://github.com/wbthomason/packer.nvim), so I put 
  ```
  use 'lervag/vimtex'
  ```
  in my `plugins.lua`. VimTex is a filetype plugin for .tex files that makes it much easier to actively compile LaTeX files in Neovim. Simply run `:VimtexCompile` while in a LaTeX file and you should see your default PDF reader open with the compiled PDF. I bound this to `<leader>ll` for easier access.
  ```
  keymap("n", "<leader>ll", ":VimtexCompile<CR>", opts)
  ```
  The second plugin that I use is a snippets plugin called [LuaSnip](https://github.com/L3MON4D3/LuaSnip). In Gilles Castel's article, he uses UltiSnips, which is written in Vimscript. You can use either, but I prefer Luasnip because the rest of my config is written in Lua. Install LuaSnip with 
  ```
  use 'L3MON4D3/LuaSnip'
  ```
  Luasnip allows me to type otherwise complicated Lua functions with only a few keypresses. For example, `beg` expands to 
  ```
  \begin{}
    
  \end{}
  ```
  These various snippets are ported over from Gilles' UltiSnips and are packaged at a repository over on [Github](https://github.com/iurimateus/luasnip-latex-snippets.nvim). Install them with 
  ```
  use 'iurimateus/luasnip-latex-snippets.nvim'
  ```
  
  Now that you have set up Neovim to work well with LaTeX, it's time to start learning the language. In the next part of this series, I will go over the basics of LaTeX and a few tricks I use involving VimTex and snippets. Now go learn some LaTeX.
