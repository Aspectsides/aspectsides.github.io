---
title: "Desktop Icons in AwesomeWM"
date: 2023-02-07T23:06:15-08:00
draft: false
---

Yes, I know what you're going to say. A Linux user, with *desktop icons* on his desktop? Blasphemy! And you're right. It is blasphemy. I still do it, though. I mean, it's not like my desktop looks like this.

![hell](/hell.jpg "Hell.")

That's just wrong. I believe that as long as you put only what you really need on your desktop, it's only slightly blasphemy. This is what my AwesomeWM desktop looks like:

![nice](/nice.png "Heaven.")

As you can see, despite having *gags* desktop icons on the screen, it still looks quite clean. I ran into a few snags while attempting to set up desktop icons in Awesome, so I decided to write a short blog post about the process

First things first, there are two file managers that I know of that support desktop icons out of the box, those being Nemo and PCManFM. I use Nemo, and I would use Nemo over PCManFM because it supports GTK3 as opposed to GTK2 and is still being actively maintained. Install Nemo with 
```
sudo pacman -S nemo
```

Nemo comes with a nifty little command called `nemo-desktop` which adds the contents of `~/Desktop` to your desktop. If you run it now, desktop icons will not appear. You need to turn them on with 
```
gsettings set org.nemo.desktop show-desktop-icons true
```

I would recommend putting `nemo-desktop` in your startup script for convenience sake. The problem with using Awesome with this is that it treats `nemo-desktop` as any other client, which means it can only be available on one tag, and not any others. I fixed this by adding a ghost tag that is not visible on the taglist as follows
```
screen.connect_signal("request::desktop_decoration", function(s)
	awful.tag({ "1", "2", "3", "4", "5", "6", " " }, s, awful.layout.layouts[1])
end)
```

and making `nemo-desktop` sticky, which means it shows on all desktops
```
ruled.client.append_rule {
    id = "desktop",
    rule_any = {
        class = {
        "Nemo-desktop"
        }
    },
    properties = { sticky = true, tag = " " }
}
```

One downside (well, not really a downside for me) is that Nemo has it's own root menu, which means you won't be able to use your own root menu. This is fine by me because my root menu is still Awesome's default root menu, and Nemo's root menu is actually pretty good, integrating well with Nemo itself.

I think desktop icons are really comfy, and add a little bit of uniqueness to a rice. Hopefully this post is easy enough to follow so that you can get started adding your own desktop icons.
