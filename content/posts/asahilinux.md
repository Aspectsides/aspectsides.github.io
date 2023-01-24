---
title: "How I installed Arch Linux on an M1 Macbook Air"
date: 2023-01-23T16:20:00-08:00
draft: false
---
# How I installed Arch Linux on an M1 Macbook Air

# What is Asahi Linux?

Asahi Linux is an Arch-Based distribution of Linux that is specifically designed for use on MacBooks with Apple Silicon processors. It is, weirdly enough, *faster* than MacOS on the same hardware. As someone who's only computer is an M1 MacBook Air, I have long been looking for something like this. I installed Asahi back in May of 2022, and it was not a great experience, mainly because of the inability to suspend the system and the lack of GPU drivers, which made it impossible to change the brightness. This meant that I was either staring into a black void with the screen off or staring into the surface of the Sun. At the beginning of December 2022, however, GPU drivers were released on the Asahi Edge kernel, and I decided to try out Asahi again. I installed Qtile, riced it out a little, and it has become my daily driver. Here is how I did it.

# Installing Asahi

Installing Asahi is incredibly simple, requiring only one line to be pasted into the terminal. Make sure your system is updated to at least MacOS 12.3, then open a terminal and run: `curl https://alx.sh | sh` Go through the options, making sure not to select expert mode and allocating your desired amount of space to Asahi. As long as you follow the instructions in the installation script you should be completely fine. After the installation is complete, it will prompt you to shut down your computer. *Make sure to wait until your computer is fully shut down*, then press and hold the power button until you see "startup options loading." When you see the startup options, select Asahi Linux to boot into it. You will be prompted to enter your root username and password, which should just be the username and password you have been using on MacOS. Follow the rest of the installation process, and you will be greeted by Asahi Linux in the KDE Desktop environment.

# Installing Dependencies and the Asahi-Edge Kernel

The first thing we are going to do is install the Asahi-Edge kernel. This is the kernel that contains the ability to suspend your computer as well as the GPU drivers. Following the instructions shown on Asahi Linux's official blog post, run the following commands to update your system and install the edge kernel:

```
$ sudo pacman -Syu
$ sudo pacman -S linux-asahi-edge mesa-asahi-edge
$ sudo update-grub
```

Before we reboot our computer and log in to the new kernel, we are going to install some dependencies. One essential thing for any Arch user is to install an AUR helper. I use paru, so to install it run these commands:

```
sudo pacman -S --needed base-devel
git clone https://aur.archlinux.org/paru.git
cd paru
makepkg -si
```

Now we can use paru to install all the things we need. `paru -S rofi alacritty qtile-git qtile-extras-git chromium lf pcmanfm dunst picom-ibhagwan-git fish emacs-git networkmanager blueman light nitrogen` Now that you have all that installed, you face one of two choices; either copy and paste my dotfiles over from my
=> https://github.com/Aspectsides/archfiles github repo
by running

```
git clone https://github.com/Aspectsides/archfile
cd archfiles
cp -r .config/* ~/.config
```

*or* you could write your own config files. Lemme give you a few tips if you decide to do this.

# Janky fixes for problems (this is what I get for trying to run Linux on Mac)

By default, there are a few problems with running Qtile as a window manager instead of something like Gnome or KDE, such as the inability to gracefully connect to Wifi or Bluetooth, or even change your volume or brightness with the built-in MacOS volume and brightness keys. We are going to work our way around that.

### Wifi and Bluetooth (also wallpaper)

These are relatively simple fixes. Install networkmanager and blueman using paru by running `paru -S networkmanager blueman` and setting your window manager to run nm-applet and blueman-applet on startup. In Qtile's `autostart.sh` this looks something like this.

```
#!/usr/bin/env bash
nm-applet &
nitrogen --restore &
blueman-applet &
```

This will add Wifi and Bluetooth icons to your systray if you have one. If you are using my dotfiles, this is on the internal Qtile bar. Make sure to call `autostart.sh` when you start up Qtile by putting this in your `config.py`

```
@hook.subscribe.startup_once
def start_once():
    home = os.path.expanduser("~")
    subprocess.call([home + "/.config/qtile/autostart.sh"])
```

Now it should be easy to connect to WiFi or Bluetooth simply by clicking on the icon in the systray.  To set a wallpaper in Qtile, I use nitrogen, which should already be installed. All you need to do is run `nitrogen ~/directory_to_wallpapers` and choose a wallpaper.

### Volume and Brightness

In order to use MacOS's keyboard to control volume, I put this in my `config.py`

```
    Key(
        [],
        "XF86AudioRaiseVolume",
        lazy.spawn("pactl set-sink-volume @DEFAULT_SINK@ +5%"),
        desc="Increase volume",
    ),
    Key(
        [],
        "XF86AudioLowerVolume",
        lazy.spawn("pactl set-sink-volume @DEFAULT_SINK@ -5%"),
        desc="Decrease volume",
    ),
```

This is by no means an elegant method, since it only changes the volume for the audio sink that is currently being used, but it is the only thing that worked for me. Brightness is a bit more problematic because of the nature of the graphics driver. As far as I know, the only way to change the brightness of the display is to do it from KDE itself. In order to change the brightness in Qtile, I had to use the third party program known as light. It should already be installed, so just add this into your config.py

```
    Key(
        [],
        "XF86MonBrightnessUp",
        lazy.spawn("light -A 1"),
        desc="Brightness Up",
    ),
    Key(
        [],
        "XF86MonBrightnessDown",
        lazy.spawn("light -U 1"),
        desc="Brightness Down",
    ),
```

### Using Spotify and Discord

The official clients for Spotify and Discord are not available on the aarch64 architecture, so we're gonna need some alternatives. I include this part because my only friends are on Discord and I physically cannot work with music, so these two apps are very important to me. Fortunately, this is a pretty easy fix. For Discord, just install ArmCord, a Discord client made specifically for the Arm64 architecture. Install it with `paru -S armcord-bin`. For Spotify, I use Spotify-TUI in combination with Spotifyd to play music using Spotify's API. I'm not gonna cover the installation process here, but [this](https://www.youtube.com/watch?v=TaPWqXFtce8) is a really good video tutorial on this exact topic.

# Final Thoughts

Now that GPU drivers have been released for Asahi Linux, it is truly a viable OS for daily driving on a Mac. I have had a really good experience with it over the past few days, and I strongly encourage you to go and try it out.
