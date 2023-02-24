---
title: "Self Hosting Your Own Search Engine"
date: 2023-02-23T09:17:43-08:00
categories:
  - Selfhosting
  - Privacy
draft: false
---

  You need to host your own search engine. Why? Because Google, Microsoft, even DuckDuckGo, who has a [weird relationship](https://www.msn.com/en-us/news/technology/duckduckgo-in-hot-water-over-hidden-tracking-agreement-with-microsoft/ar-AAXILR1) with Microsoft, are *all* tracking you. In fact, Google itself has said that it stores more than an *exabyte* of *your* data. That's kinda creepy. Even though most of us have nothing to hide from Google (right?), we could all do with a bit more privacy. For just ten minutes of your time, and a payment of pocket change every month, you'll be able to host your own search engine, along with a bunch of other stuff which I will cover in future guides. The search engine we will be hosting today is a meta search engine called SearXNG, which pulls results from all the major search engines and compiles them into a list of results. Since you are self hosting it, none of your data is being leaked to Google. That is an absolute win in my opinion.

## Step 1: Getting a VPS
  
  Though you can host this on your own server, it is much easier to do so on a VPS, because most come with an IPv4 address built in, which means you won't have to set up a reverse proxy. I will be doing this on a Digital Ocean droplet, because free student money. Getting a Digital Ocean droplet is really simple. Just sign up for a Digital Ocean account, give them all your payment info, and create a new droplet by clicking the very obvious green button in the top right. The cheapest plan will be more than enough, even if you plan to host a Nextcloud or VPN on it later. After you create your droplet, you should be able to see your droplet's ipv4 address. In a terminal, run 
```
ssh root@<your ipv4 address>
```
After entering the root password specified on setup, you should be greeted by your droplet's terminal. 

## Step 2: Installing Dependencies

When setting up a new server, it's always good practice to update the system. Run
```
sudo apt update && sudo apt upgrade
```
We are going to be hosting our SearX instance through Docker, so go ahead and install that and Docker Compose with
```
sudo apt install docker.io docker-compose
```
You should now be all set to begin setting up SearX.

## Step 3: Setting Up SearX

In your domain's control panel, add an A record that points to your droplet's ipv4 address. Then, SSH back into your server and download the SearX docker image. 
```
git clone https://github.com/searxng/searxng-docker.git
```
Navigate to the directory using `cd searxng-docker` and edit the .env file using `nano .env`. Change the SEARX_HOSTNAME field to your domain, and the LETSENCRYPT_EMAIL to your email address. This docker image sets up an SSL certificate for you, which is pretty cool. Now, use this command to generate a private key that is then placed into your .env file.
```
sed -i "s|ultrasecretkey|$(openssl rand -hex 32) |g" searxng/settings.yml
```
Finally, to run the Docker container, run 
```
sudo docker-compose up -d
```
Congratulations! If you navigate to your domain now, you should see SearX sitting there, looking pretty. You've successfully hosted your own SearXNG instance.
