+++
title = "Pi-Hole: Blocking Ads at the Network Level with Docker"
date = "2023-02-26T21:15:48-08:00"
author = "Daniel Xu"
authorTwitter = "" #do not include @
cover = "pihole.webp"
tags = ["pihole", "selfhost"]
keywords = ["", ""]
description = "ADS BEGONE!"
showFullContent = false
readingTime = false
hideComments = false
color = "" #color from the theme settings
+++

## Introduction

If you're tired of seeing ads on your devices while browsing the internet, Pi-Hole might be the solution you're looking for. Pi-Hole is a network-level ad and tracker blocker that blocks ads and trackers before they even reach your device. It works by redirecting DNS requests to a black hole, preventing ads and trackers from loading. In this post, we'll learn how to set up Pi-Hole using Docker.

## What is Docker?

Docker is an open-source platform that allows developers to package applications into containers. Containers are lightweight, self-contained environments that can run anywhere, making it easy to deploy applications. Docker is widely used in the industry to deploy and manage applications, and it can be used to set up Pi-Hole as well.

## Setting up Pi-Hole with Docker

To set up Pi-Hole with Docker, you'll need to have Docker installed on your machine. Once you have Docker installed, you can run the following command to download and run the Pi-Hole Docker container:

```bash
docker run -d \\
    --name pihole \\
    -p 53:53/tcp -p 53:53/udp \\
    -p 80:80 \\
    -p 443:443 \\
    -e TZ="America/New_York" \\
    -e WEBPASSWORD={password} \\
    -v "/etc/pihole/:/etc/pihole/" \\
    -v "/etc/localtime:/etc/localtime:ro" \\
    --restart=unless-stopped \\
    pihole/pihole:latest

```

This command will download and run the latest version of the Pi-Hole Docker container. It will also map the necessary ports and volumes, set the time zone, and set the web password. Make sure to replace `{password}` with a strong password.

Once the container is running, you can access the Pi-Hole web interface by going to `http://<docker-host-ip>/admin`. You should see the Pi-Hole dashboard, which will show you the number of blocked ads and trackers.

## Blocklists

Blocklists are an essential component of Pi-Hole, as they allow the software to block unwanted connections to your network. These blocklists are essentially lists of domains that are known to be associated with adware, malware, and other unwanted connections that can slow down your network and compromise your security.

One popular blocklist that many Pi-Hole users rely on is Oisd. This blocklist contains a vast number of domains that have been identified as sources of unwanted connections, making it a comprehensive and effective option for those looking to protect their network. You can find Oisd at [https://big.oisd.nl/domains](https://big.oisd.nl/domains).

While Oisd is an excellent choice for many users, some may choose to add additional blocklists to further enhance their network's security. It's important to note, however, that adding too many blocklists can cause Pi-Hole to become less effective, as it may end up blocking legitimate connections along with unwanted ones. Therefore, it's essential to find the right balance of blocklists that works best for your particular network.

## Conclusion

Pi-Hole is a powerful ad and tracker blocker that can help you protect your privacy and block annoying ads. By setting it up with Docker, you can easily deploy and manage Pi-Hole on your network. Give it a try and enjoy a cleaner, faster browsing experience!
