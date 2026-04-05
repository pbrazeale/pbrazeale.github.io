+++
tags = ['OpenClaw', 'OpenShell', 'AI', 'Proxmox', 'Linux', 'Build Notes', 'Security+', 'Docker', 'Open Source']
title = 'OpenClaw Build Notes: From Debian Laptop Notes to a Real AI Lab Stack'
date = 2026-04-05T14:14:07+01:00
draft = true
+++

My first [NemoClaw setup on a ThinkPad T14s running Debian 13.4](https://pbrazeale.github.io/posts/nemoclaw-setup/) was a success.

Not a polished success; not an enterprise success; not even a “you should definitely deploy this the same way I did” success.

**But it was a real success.**

It answered the question that mattered at the time: can I get OpenShell, OpenClaw, and NemoClaw running on real Linux hardware, outside the clean-room fantasy of vendor demos and idealized docs?

Yes.

And once that answer became yes, the next question showed up immediately: Can I operate this stack sanely, repeatedly, and safely?

**That is a different question altogether.**

## Proof-of-Life Matters

Early experiments do not need to be elegant; they need to be real.

That first laptop build did exactly what it was supposed to do. It proved Debian was viable. It proved I did not need to wait for some polished, enterprise-sanctioned golden path before getting hands on keyboard. It let me stop reading about the stack and start interacting with it directly; which, in this new era, is where most actual learning begins.

It also proved something more important than “it boots.”

It proved this stack was worth building around.

And the docs now confirm one of the key pain points I hit on that first round, because it turns out it was not a personal failure at all. It was a product limitation:

> Sandbox browser is not supported on the OpenShell backend. [Source][2]

That one line matters more than it may seem. It reframes the laptop experiment as proof-of-life, not failed architecture.

The point was not to squeeze a permanent lab out of one Debian machine. The point was to learn enough to know what the next layer of infrastructure needed to be.

## T14 Experiment Takeaways

For my part, I still think the laptop route was the correct opening move.

It was cheap. It was immediate. It was close to the metal. It let me validate Docker on Debian 13, get OpenShell installed, walk through the NemoClaw flow, and start thinking in terms of agents, workspaces, policies, tool boundaries, and swarm design.[1][2][7]

That is a meaningful threshold.

Once you cross it, though, the machine stops being “a laptop running some tools” and starts becoming “the place where I’m trying to host an emerging AI lab.” That distinction sounds semantic; it isn’t. It is the difference between experimentation and operations.

And operations demand boundaries.

### The Stack Stopped Being a Toy

This is the same broader point I’ve been circling in my recent Vibe Coding posts.

When AI increases the amount one person can attempt, the bottleneck shifts. The hard part stops being whether you can generate code, wire tools together, or brute-force a setup script into submission. The hard part becomes whether the system around that speed is structured enough to survive it.

In other words: higher velocity demands more guardrails, not fewer.

That is true for software teams. It is also true for solo builders trying to stand up agent systems.

The more autonomy you unlock, the more your environment design starts to matter.

And that is exactly where my Debian laptop stopped being “good enough.”

## Debian Laptop -> Proxmox Serve

A laptop is excellent for proof-of-life. It's not a great long-term substrate for an agent lab. _I'm not sure my single proxmox server is enough either, as it runs my home services. Might be time to buy a 2nd sever on ebay!_

### Session fragility

When you are running gateway processes, shells, browser-linked tooling, Docker services, and experiments over SSH, you eventually discover the difference between _I can keep this alive_ and _I can trust this to stay alive_.

Tmux helps (and I still love tmux), but tmux is not infrastructure. It is a coping mechanism for a machine that is doing too many jobs at once, and doesn't offer an intuitive interface. _Or else, I'm just not terminal native, and it's really a skill issue LOL_

### Resource contention

Your primary workstation should not also be your lab floor.

The same machine becomes your editor, your browser, your Docker host, your test box, your SSH jump point, and your agent runtime. Chrome fights containers. Containers fight local tooling. CPU core limits, RAM pressure, and attention all become shared resources.

The machine you need for thinking becomes the machine you are actively destabilizing.

### Reproducibility decay

This is the one that always gets you eventually.

A laptop accumulates scar tissue. One-off fixes pile up. PATH hacks linger. Package state drifts. Half-remembered shell tweaks become “part of the setup,” even though they were never part of the setup at all. (_Rebuilding the environment stops being a clean exercise and starts becoming archaeology._)

### Isolation gets harder as the swarm grows

One agent is easy to improvise around.

A swarm is not.

The moment you want a stable OpenClaw environment, a browser-heavy test box, a Portainer VM, and a throwaway experiment machine all at once, the “just run it on my main Debian box” approach starts looking sloppy.

Then add atop this the need to have not 1, but 10+ agents running, and all needing the same support infra, and you'll start to understand my panic. Support needs its own sever and hardware allocation.

I run my homelab on a HP Z440; a brilliant little machine that's gotten me this far. However, she only has a Xeon E5-2680 (that's 8 core and each agent needs 2, ideally 4) and 64GB ram (each agent needs 8, ideally 16) and this is before we get to the supporting infra and the fact that 32GB and 8 cores are already allocated. I can over allocate on the RAM and live, but I don't want to do so on the CPU.

#### New Server HP Z8 G4 or G5

This will cost more than my bike did brand new, but I ought to recoup this with my first project.
