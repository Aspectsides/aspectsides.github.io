+++
title = "Self Hosting a Media Server with Jellyfin"
date = "2023-02-26T14:00:53-08:00"
author = "Daniel Xu"
authorTwitter = "" #do not include @
cover = "jellyfin.jpg"
tags = ["selfhosting", "homelab"]
keywords = ["", ""]
description = "No Netflix? No Problem!"
showFullContent = false
readingTime = false
hideComments = false
color = "" #color from the theme settings
+++

## Introduction

With the rise of streaming services such as Netflix and Hulu, it might seem like owning a physical media collection is a thing of the past. However, for many people, owning and managing their own collection of movies, TV shows, and music is still an important part of their media consumption. If you're one of these people, you might be interested in self-hosting a media server. In this blog post, we'll be discussing Jellyfin, a free and open-source media server that you can use to host your own media collection.

## What is Jellyfin?

Jellyfin is a media server that allows you to stream your own media collection to a variety of devices. It is free and open-source, which means that anyone can download and use it without paying anything. One of the great things about Jellyfin is that it is completely customizable. You can choose which media formats are supported, which devices can access your server, and even customize the look and feel of the user interface.

## Setting up Jellyfin

Setting up Jellyfin is relatively simple. First, you'll need a computer running Linux. My server is running Ubuntu Server Edition, mainly because I’m just too lazy to install anything else. If you haven’t already, you’ll also need to install Docker. Run

```bash
sudo apt update && sudo apt upgrade
sudo apt-get install docker.io -y
sudo apt-get install docker-compose -y
```

This will update your system and install both Docker Community Edition and Docker-Compose, which is a really handy tool for writing more complex Docker commands.

Next, you’ll want to create directories to store your media collection in. I have a directory called media in my home directory, in which I created two folders; movies and shows.

Now, in a directory of your choice, create a file called `docker-compose.yml` and paste this in there:

```yaml
---
version: "2.1"
services:
  jellyfin:
    image: lscr.io/linuxserver/jellyfin:latest
    container_name: jellyfin
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Etc/UTC
      - JELLYFIN_PublishedServerUrl=192.168.0.5 #optional
    volumes:
      - /path/to/library:/config
      - /path/to/tvseries:/data/tvshows
      - /path/to/movies:/data/movies
    ports:
      - 8096:8096
      - 8920:8920 #optional
      - 7359:7359/udp #optional
      - 1900:1900/udp #optional
    restart: unless-stopped    
```

Replace “user” in the media volume with your username. Now, in the same directory, run 

```bash
sudo docker-compose up -d
```

Your Jellyfin instance should now be accessible at <your server’s ip address>:8096.

## Using Jellyfin

Once you've set up Jellyfin, you can start streaming your media collection to your devices. You can access your media server through a web browser by going to the aforementioned url, or by downloading one of the many Jellyfin apps that are available for different devices. With Jellyfin, you can stream your media to a variety of devices, including smartphones, tablets, smart TVs, and even gaming consoles. You can also customize the user interface to make it look and feel the way you want it to.

## Conclusion

Self-hosting a media server with Jellyfin is a great way to take control of your media collection. With Jellyfin, you can stream your media to a variety of devices, and customize the server settings to fit your needs. If you're interested in self-hosting a media server, Jellyfin is definitely worth checking out. Best of all, it's completely free and open-source, so you can try it out without any financial commitment.
