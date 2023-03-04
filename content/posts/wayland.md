+++
title = "Sway"
date = "2023-03-03T23:25:23-08:00"
author = "Daniel Xu"
authorTwitter = "" #do not include @
cover = "sway.png"
tags = ["unix", "ricing"]
keywords = ["", ""]
description = "NO MORE SCREEN TEARING"
showFullContent = false
readingTime = false
hideComments = false
color = "" #color from the theme settings
draft = true
+++

# Big Text

Baby seals.

```shell
# Autostart
exec udiskie
exec gammastep
exec mako
output eDP-1 scale 1.5
exec_always autotiling 
exec rm -f /tmp/sovpipe && mkfifo /tmp/sovpipe && tail -f /tmp/sovpipe | sov -t 300

# Style
font pango:mononoki Nerd Font 14px 
titlebar_border_thickness 0
gaps inner 7
gaps outer 7
default_border pixel 0
default_floating_border pixel 0

# Defining colors         border     bg         text       indicator  child_border
client.focused        	 	#12151d    #12151d    #abb2bf    #c678dd    #12151d
client.unfocused        	#1e222a    #1e222a    #abb2bf	 #282c34    #282c34
client.focused_inactive 	#1e222a    #1e222a    #abb2bf    #282c34    #282c34
client.urgent	          	#e06c75    #1e222a    #abb2bf    #e06c75    #e06c75

# Import GTK settings
set $gnome-schema org.gnome.desktop.interface

exec_always {
    gsettings set $gnome-schema gtk-theme 'Everblush'
    gsettings set $gnome-schema icon-theme 'Tokyonight-Dark'
    gsettings set $gnome-schema cursor-theme 'Bibata-Modern-Classic'
}


# Window rules
for_window [app_id="ncmpcpp"] floating enable, resize set height 400 px, resize set width 800 px, move position 1080 5
for_window [app_id="cava"] floating enable, resize set height 400 px, resize set width 800px, move position 5 590
for_window [app_id="libera"] floating enable, resize set height 500 px, resize set width 900px, move position 980 5
for_window [app_id="tilde"] floating enable, resize set height 500 px, resize set width 900px, move position 5 490
for_window [app_id="low-key"] floating enable, resize set height 400 px, resize set width 800px, move position 220 150
for_window [app_id="veracrypt"] floating enable

# Assignments
assign [app_id="amfora"] 2
assign [app_id="neomutt"] 4
assign [app_id="libera"] 6
assign [app_id="tilde"] 6
assign [app_id="low-key"] 6
assign [app_id="telegramdesktop"] 4
assign [class="Signal Beta"] 4
assign [app_id="org.pwmt.zathura"] 5
assign [class="Gimp-2.10"] 7
assign [class="Krita"] 7
assign [app_id="audacity"] 8
assign [app_id="audacity"] 8
assign [app_id="ncmpcpp"] 10
assign [app_id="cava"] 10

# Keybindings

## Touchpad settings
input "1739:52545:SYNA7DB5:01_06CB:CD41_Touchpad" {
       dwt enabled
       tap enabled
       natural_scroll enabled
       middle_emulation enabled
   }

# or input <identifier>
input "type:keyboard" {
    xkb_options caps:escape
}

## Logo key
set $mod Mod4

## Home row direction keys
set $left h
set $down j
set $up k
set $right l

# Defaults

## terminal emulator
set $term foot

## Your preferred application launcher
# Note: pass the final command to swaymsg so that the resulting window can be opened
# on the original workspace that the command was run on.
for_window [app_id="^launcher$"] floating enable, sticky enable, resize set 30 ppt 60 ppt, border pixel 10
# set $menu wofi --hide-scroll | xargs swaymsg exec --
set $menu exec $term -a launcher -e sway-launcher-desktop

## Output configuration
# Default wallpaper 
# output * bg /home/loki/pictures/wallpapers/mountain-rocks-at-sea.jpg fill
# output * bg /home/aspect/Pictures/Wallpapers/patience_catppuccin.png fill
output * bg /home/aspect/Pictures/Wallpapers/stairs.jpg fill


# Behavior
focus_follows_mouse yes

### Idle configuration
#
# Example configuration:
#
 exec swayidle -w \
          timeout 600 '/home/aspect/.local/bin/lock.sh -f' \
          timeout 1800 'swaymsg "output * dpms off"' resume 'swaymsg "output * dpms on"' \
          before-sleep '/home/aspect/.local/bin/lock.sh -f'

# This will lock your screen after 300 seconds of inactivity, then turn off
# your displays after another 300 seconds, and turn your screens back on when
# resumed. It will also lock your screen before your computer goes to sleep.

# Key bindings
#
# Basics:
#
# Start a terminal
bindsym $mod+Return exec $term

# Start Emacs
bindsym $mod+e exec emacs

# Kill focused window
bindsym $mod+q kill

# Start your launcher
bindsym $mod+space exec $menu

# Dismiss notifications
bindsym Control+space exec makoctl dismiss

# Screenshot with grim and swappy
bindsym $mod+shift+s exec grim - | swappy -f -
bindsym $mod+control+s exec grim -g "$(slurp)" - | swappy -f -
    # Drag floating windows by holding down $mod and left mouse button.
    # Resize them with right mouse button + $mod.
    # Despite the name, also works for non-floating windows.
    # Change normal to inverse to use left mouse button for resizing and right
    # mouse button for dragging.
    floating_modifier $mod normal

# Reload the configuration file
bindsym $mod+Shift+c reload

# Exit sway (logs you out of your Wayland session)
bindsym $mod+Shift+e exec swaynag -t custom -m 'Do you wish to fully reload your Sway session?' -b 'Yes' 'swaymsg exit'
# Turn the system off
bindsym $mod+Shift+p exec swaynag -t custom -m 'What action would you like to perform?' -b 'Shutdown' 'poweroff' -b 'Restart' 'poweroff --reboot'
bindsym $mod+p exec wlogout
#
# Moving around:
#
# Move your focus around
bindsym $mod+$left focus left
bindsym $mod+$down focus down
bindsym $mod+$up focus up
bindsym $mod+$right focus right

# Move the focused window with the same, but add Shift
bindsym $mod+Shift+$left move left
bindsym $mod+Shift+$down move down
bindsym $mod+Shift+$up move up
bindsym $mod+Shift+$right move right
#
# Workspaces:
#
# Switch to workspace
bindsym --no-repeat $mod+1 workspace number 1; exec "echo 1 > /tmp/sovpipe"
bindsym --no-repeat $mod+2 workspace number 2; exec "echo 1 > /tmp/sovpipe"
bindsym --no-repeat $mod+3 workspace number 3; exec "echo 1 > /tmp/sovpipe"
bindsym --no-repeat $mod+4 workspace number 4; exec "echo 1 > /tmp/sovpipe"
bindsym --no-repeat $mod+5 workspace number 5; exec "echo 1 > /tmp/sovpipe"
bindsym --no-repeat $mod+6 workspace number 6; exec "echo 1 > /tmp/sovpipe"
bindsym --no-repeat $mod+7 workspace number 7; exec "echo 1 > /tmp/sovpipe"
bindsym --no-repeat $mod+8 workspace number 8; exec "echo 1 > /tmp/sovpipe"
bindsym --no-repeat $mod+9 workspace number 9; exec "echo 1 > /tmp/sovpipe"
bindsym --no-repeat $mod+0 workspace number 10; exec "echo 1 > /tmp/sovpipe"

bindsym --release $mod+1 exec "echo 0 > /tmp/sovpipe"
bindsym --release $mod+2 exec "echo 0 > /tmp/sovpipe"
bindsym --release $mod+3 exec "echo 0 > /tmp/sovpipe"
bindsym --release $mod+4 exec "echo 0 > /tmp/sovpipe"
bindsym --release $mod+5 exec "echo 0 > /tmp/sovpipe"
bindsym --release $mod+6 exec "echo 0 > /tmp/sovpipe"
bindsym --release $mod+7 exec "echo 0 > /tmp/sovpipe"
bindsym --release $mod+8 exec "echo 0 > /tmp/sovpipe"
bindsym --release $mod+9 exec "echo 0 > /tmp/sovpipe"
bindsym --release $mod+0 exec "echo 0 > /tmp/sovpipe"
# Move focused container to workspace
bindsym $mod+Shift+1 move container to workspace number 1
bindsym $mod+Shift+2 move container to workspace number 2
bindsym $mod+Shift+3 move container to workspace number 3
bindsym $mod+Shift+4 move container to workspace number 4
bindsym $mod+Shift+5 move container to workspace number 5
bindsym $mod+Shift+6 move container to workspace number 6
bindsym $mod+Shift+7 move container to workspace number 7
bindsym $mod+Shift+8 move container to workspace number 8
bindsym $mod+Shift+9 move container to workspace number 9
bindsym $mod+Shift+0 move container to workspace number 10
# Note: workspaces can have any name you want, not just numbers.
# We just use 1-10 as the default.
bindsym $mod+Tab workspace back_and_forth
#
# Layout stuff:
#
    # You can "split" the current object of your focus with
    # $mod+b or $mod+v, for horizontal and vertical splits
    # respectively.
    bindsym $mod+b splith
    bindsym $mod+v splitv

    # Switch the current container between different layout styles
    bindsym $mod+m layout tabbed
    bindsym $mod+t layout toggle split

    # Make the current focus fullscreen
    bindsym $mod+f fullscreen

    # Toggle floating 
    bindsym $mod+s floating toggle
    # Toggle between floating and other layout
    bindsym $mod+Shift+f focus mode_toggle
    # Move floating windows around
    bindsym $mod+Up move up 1
    bindsym $mod+Shift+Up move up 10
    bindsym $mod+Left move left 1
    bindsym $mod+Shift+Left move left 10
    bindsym $mod+Right move right 1
    bindsym $mod+Shift+Right move right 10
    bindsym $mod+Down move down 1
    bindsym $mod+Shift+Down move down 10

    # Move focus to the parent container
    bindsym $mod+a focus parent

    # Move focus to the child container
    bindsym $mod+Shift+a focus child
#
# Scratchpad:
#
    # Sway has a "scratchpad", which is a bag of holding for windows.
    # You can send windows there and get them back later.

    # Move the currently focused window to the scratchpad
    bindsym $mod+Shift+minus move scratchpad

    # Show the next scratchpad window or hide the focused scratchpad window.
    # If there are multiple scratchpad windows, this command cycles through them.
    bindsym $mod+minus scratchpad show

# Resizing containers:
bindsym $mod+alt+$left resize shrink width 20px
bindsym $mod+alt+$up resize grow height 20px
bindsym $mod+alt+$down resize shrink height 20px
bindsym $mod+alt+$right resize grow width 20px

## Special keys
bindsym --locked XF86AudioRaiseVolume exec sh -c "~/.local/bin/changevolume up"
bindsym --locked XF86AudioLowerVolume exec sh -c "~/.local/bin/changevolume down"
bindsym --locked XF86AudioMute exec pactl set-sink-mute 45 toggle
bindsym XF86MonBrightnessUp exec light -A 10 && notify-send "󰃞 Light" "Brightness: $(light)%" --hint="int:value:$(light)"
bindsym XF86MonBrightnessDown exec light -U 10 && notify-send "󰃞 Light" "Brightness: $(light)%" --hint="int:value:$(light)"
bindsym --locked XF86AudioPlay exec mpc toggle
bindsym --locked XF86AudioNext exec mpc next
bindsym --locked XF86AudioPrev exec mpc prev
bindsym --locked $mod+d exec sh -c "notify-send 'Do Not Disturb' 'Turning on Do Not Disturb Mode'; sleep 2; makoctl set-mode do-not-disturb"
bindsym --locked $mod+Shift+d exec sh -c "makoctl set-mode default ; notify-send 'Do Not Disturb' 'Do Not Disturb Mode disabled'"

# Status Bar:
# Read `man 5 sway-bar` for more information about this section.
bar {
    swaybar_command waybar
    }
}



input * repeat_delay 180
input * repeat_rate 50
include /etc/sway/config.d/*
```

