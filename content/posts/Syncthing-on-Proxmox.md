+++
tags = ['Home Lab', 'Virtual Environment', 'Linux', 'Articles', 'Proxmox', 'Obsidian']
title = 'Syncthing LXC on Proxmox'
date = 2025-09-20T09:01:07+01:00
draft = false
+++

## ![Syncthing on Proxmox](https://pbrazeale.github.io/images/syncthing_on_proxmox.jpg)

## Syncthing LXC Script

[Proxmox VE Helper-Scripts](https://community-scripts.github.io/ProxmoxVE/scripts?id=syncthing)

This is a huge timesaver! The community is amazing for building out these helper scripts and their TUIs (terminal user interfaces) are fantastic for quickly altering the setup settings.

My core need was to sync files between my work laptop and personal desktop without allowing the laptop access to my server directly. [Syncthing](https://syncthing.net/) solves this problem perfectly, as it's encrypted at rest, password protected at each access point, and isolates the directory access to only the exact files I want. Brilliant!

If you've never looked into Syncthing you should.

### Settings

I chose to go with 2 cpu cores, 2 GB RAM, and 1 GB HD space. Proxmox makes it easy to boost LXCs if I under allocate resources, but based on the initial sync, I think if anything I over allocated LOL.

Bridging the data from TrueNAS to the Syncthing LXC was easy. I just refollowed my own guide: [TrueNAS to Proxmox to LXC](https://pbrazeale.github.io/posts/truenas-to-proxmox-to-lxc/)

### Obsidian

If you're not writing your own guides and technical notes, check out my [9 Months Obsidian Takeaways](https://pbrazeale.github.io/posts/9-months-obsidian-takeaways/). I literally list Obsidian as one of my core technologies in my development stack, because without the quick access to my notes, I'd be half the software engineer.

This is precisely why I had to get Syncthing setup. I've been meaning to figure out a solution since I started my new job, but one thing after another happened and I kept putting it off. However, now it's setup and I can stop using my KVM switch to flip between my laptop and desktop when I need access to notes. Or worse, emailing myself the notes for quick reference. (_Bad tech professional LOL_)

### Issues

Thus far the only thing I ran into is that the server threw up an error about not being able to sync. I went to Synthing folder listing on the server IP:

- Edit
- Advanced
- selected "Ignore Permissions"

That seems to have fixed the issue, but obviously I'll keep a very close eye on my notes.

### Closing Thoughts

If you've not started your home lap, there's never been a better time. Hardware has dropped to stupid low pricing; like tiny footprint, energy efficient, PCs for $200-$250 that can likely run anything you need to start. And with the helper scripts and ease of use of Proxmox, it's so easy now.
