---
title: "Org Roam"
date: 2023-01-23T23:59:31-08:00
draft: false
ShowToc: true
TocOpen: true
---

# Org Roam; The New best Notetaking Software for the Zettelkasten method

## Why not Obsidian? or Vimwiki?

I have hopped notetaking software more times than I can count. When I first had the need to take notes, I did them in Google Docs and saved them to Google Drive. This was terrible, and I have no idea what by 13 year old self was doing. When I got slightly older and wiser, I discovered Evernote and transitioned over to that. And Evernote was&#x2026; fine. I have nothing negative to say about Evernote. Problem is, it&rsquo;s basically a glorified file manager that opens plain text files. And I didn&rsquo;t like that. Also, at this point, I was getting into the concept of building my own second brain, which requires the linking together of notes. And Evernote didn&rsquo;t have any intuitive way to do this. So I switched over to Notion. Then Obsidian. I really don&rsquo;t have anything negative to say about those either except that they are Electron apps, and don&rsquo;t have Vim keybindings which I was becoming increasingly reliant on those days. Then I found Vimwiki. It had everything that I wanted except for a visualizer for my second brain. I used it for a while but I needed to flex that second brain visualizer. That&rsquo;s when I found Org Roam.

## What is Org Roam?

Org roam is a replica of Roam Research for Emacs and Org Mode. It encourages the linking together of ideas and notes, and is a great tool for building your personal second brain. It comes with all the benefits and power of Org-Mode, but adds an extra layer of usability and ease of linking to your documents. Let&rsquo;s get started with installing it.

## Installation

**Disclaimer: I use a distribution of Emacs called Doom Emacs, so the following steps will be tailored for Doom.**

To install Org-Roam on Doom Emacs, in your init.el look for the line that says `org`. Then, change it to `(org +roam2)`. Run `doom sync` in your shell to reload Doom, and you should have org roam installed. There is one more thing we have to do before we start off with using Org Roam though. In your config.el, add the following line:

    (setq org-roam-directory "~/Documents/roam")

Obviously, change the directory to whatever directory you would like your roam to be stored in. Make sure the directory exists first, though.

## Using Org Roam

To create your first note, you can hit `<space> nrn` in Doom with evil keybindings. After Emacs compiles the sql database required to run Org Roam, it will open the file for you. Org Roam notes follow Org Mode syntax, so everything you can do in Org Mode is doable in Org Roam. Try adding some content to your file. In order to link to another note or create another note and link to it, you can press `<space> nri`. Type the name of the desired note and press enter. Emacs will open the note in a split which you can then finalize and insert by pressing `ctrl-c ctrl-c`. To find and open a note, you can use the key combination `<space> nrf`. This allows you to search through all your notes.

## Conclusion

This is a very barebones guide on what I think is the most powerful tool in my daily workflow right now. I will make additional articles about my workflow and the extensions I use to make my experience even more awesome, but for now I just wanted to get this out here. I&rsquo;m officially an Emacs user again.

