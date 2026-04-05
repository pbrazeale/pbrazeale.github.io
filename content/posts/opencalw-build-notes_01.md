+++
tags = ['OpenClaw', 'Docker', 'Portainer' 'OpenShell', 'AI', 'Linux', 'Build Notes', 'Security+',  'Open Source']
title = 'From Debian Laptop Notes to a Real AI Lab Stack'
date = 2026-04-05T14:14:07+01:00
draft = true
+++

My first article [NemoClaw Setup: Thinkpad T14s, Debian 13.4](https://pbrazeale.github.io/posts/nemoclaw-setup/) was a success.

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

Once you cross it, though, the machine stops being “a laptop running some tools” and starts becoming “the place where I’m trying to host an emerging AI lab.” That distinction sounds semantic; it'sn’t. it's the difference between experimentation and operations.

And operations demand boundaries.

### The Stack Stopped Being a Toy

This is the same broader point I’ve been circling in my recent Vibe Coding posts.

When AI increases the amount one person can attempt, the bottleneck shifts. The hard part stops being whether you can generate code, wire tools together, or brute-force a setup script into submission. The hard part becomes whether the system around that speed is structured enough to survive it.

In other words: higher velocity demands more guardrails, not fewer.

That is true for software teams. it's also true for solo builders trying to stand up agent systems.

The more autonomy you unlock, the more your environment design starts to matter.

And that is exactly where my Debian laptop stopped being “good enough.”

## Debian Laptop -> Proxmox Serve

A laptop is excellent for proof-of-life. It's not a great long-term substrate for an agent lab. _I'm not sure my single proxmox server is enough either, as it runs my home services. Might be time to buy a 2nd sever on ebay!_

### Session fragility

When you are running gateway processes, shells, browser-linked tooling, Docker services, and experiments over SSH, you eventually discover the difference between _I can keep this alive_ and _I can trust this to stay alive_.

Tmux helps (and I still love tmux), but tmux is not infrastructure. it's a coping mechanism for a machine that is doing too many jobs at once, and doesn't offer an intuitive interface. _Or else, I'm just not terminal native, and it's really a skill issue LOL_

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

_This will cost more than my bike did brand new, but I ought to recoup this with my first project._

The main advantage to the upgrade is I'll isolate my home services on the Z440 and the new Z8 will then become the backbone of all my AI agents and their supporting infrastructure.

## Proxmox Advantage

### Core issue this weekend

What started as an OpenClaw/OpenShell-adjacent access issue turned into a host-level networking incident. Then it happened again. The investigation path ended up including bridge checks, direct-NIC testing, neighbor-table inspection, and eventually the most humbling root cause possible: a frayed ethernet cable masquerading as a software problem.

That is exactly the sort of thing a growing lab must be designed to absorb.

Not prevent all failure; that fantasy is dead.

- But contain failure.
- Isolate it.
- Recover cleanly.
- Learn faster.

A useful lab is not one where nothing ever breaks. It's one where breakage has boundaries.

### Why Proxmox Enters the Picture

This is where [Proxmox VE](https://www.proxmox.com/en/products/proxmox-virtual-environment/overview) starts to make sense; not as a trendy homelab flex, and not as a replacement for Docker or OpenShell, but as the infrastructure layer that gives both of them room to breathe.

> Proxmox Virtual Environment is a complete, open-source server management platform for enterprise virtualization. It tightly integrates the KVM hypervisor and Linux Containers (LXC), software-defined storage and networking functionality, on a single platform. With the integrated web-based user interface you can manage VMs and containers, high availability for clusters, or the integrated disaster recovery tools with ease.

Most importantly, it gives me the thing my laptop cannot: **clean separation**.

### Separation of concerns

I do not want my daily driver to also be the blast radius for browser automation, agent sandboxes, networking experiments, and setup scripts that may or may not decide to go _interesting_ halfway through.

**With Proxmox, that separation becomes first-class.**

#### Browser Problem (Chrome or Playwright MCP)

The [OpenClaw security guidance](https://docs.openclaw.ai/gateway/security) is blunt about browser control: a model driving a real browser is powerful enough to reach whatever that browser profile can reach, and host browser control should be treated carefully; especially if you are pointing it at your daily-driver state.

That is not a reason to avoid browser workflows.

It's a reason to isolate them like an adult: [Vibe Coding for Grown-Ups](https://pbrazeale.github.io/posts/vibe-coding-01/#vibe-coding-for-grown-ups).
![4 tech jobs](https://pbrazeale.github.io/images/4-last-jobs-in-tech.webp)

Once you combine that security guidance with the fact that OpenShell currently does not support sandbox browser on that backend,[source](https://docs.openclaw.ai/gateway/openshell) the architectural answer becomes pretty obvious. Browser-heavy experimentation belongs in a dedicated environment, not smeared across the same machine that is also your primary development workstation and/or your stable lab runtime.

### Snapshots change your psychology

This is the real payoff:

- Weird setup script? Snapshot first.
- Risky Docker rework? Snapshot first.
- New browser/MCP experiment? Snapshot first.
- Fresh OpenClaw test environment? Snapshot first.

That sounds almost too obvious to say, but it matters. [Proxmox snapshots preserve VM state](https://pve.proxmox.com/wiki/Live_Snapshots); which means experimentation transform from gambling to engineering. **Rollback beats archaeology**.

### Multiple environments

A more sane design starts to appear almost immediately:

- one VM for Portainer and operational services
- one VM for a more stable OpenClaw/OpenShell/NemoClaw environment
- one VM for browser-heavy experiments and MCP tooling
- one VM for dangerous, disposable chaos

That is not complexity for its own sake. That is modularity buying back your ability to move fast without treating every test like a potential host outage. [Creating Modularity](https://pbrazeale.github.io/posts/vibe-coding-02/#creating-modularity)

## Docker

This is the part that needs to be said clearly, because otherwise people read “I’m moving to Proxmox” and hear “I’m abandoning containers.”

**I am not.**

Docker still matters; **a lot**. So much so that I'm working my way through [Docker Deep Dive by Nigel Poulton](https://www.amazon.com/dp/1916585256), to give it the time and dedication it deserves within my tech stack.

[Docker Engine](https://docs.docker.com/engine/install/debian/), and containers remain the easiest way to package, ship, rebuild, and reason about services. [Portainer](https://docs.portainer.io/start/install-ce/server/docker/linux) still matters too; its own docs are very explicit that Portainer Server and Agent run as lightweight Docker containers on a Docker engine.

So the architecture is not Docker _or_ Proxmox.

it's Docker _inside_ a Proxmox lab.

**Proxmox is the lab floor. Docker is how the machines in that lab actually work.**

That distinction matters because these tools solve different problems.

- **Proxmox** solves host-level isolation and recovery.
- **Docker** solves service packaging and runtime consistency.
- **Portainer** solves operational ergonomics for managing those containers.

They stack cleanly because they operate at different layers.

## OpenShell

The same clarification applies to OpenShell.

Per the docs, [OpenShell](https://docs.openclaw.ai/gateway/openshell) is a managed sandbox backend for OpenClaw. That is a very specific role. It governs sandbox lifecycle, remote execution, and workspace behavior for agent turns.

It's not your hypervisor, nor your datacenter layer, nor a substitute for host-level segmentation. It's the sandbox for the agent runtimes.

That is a powerful role; but it's still one layer in a larger stack.

And in practice, the OpenShell docs make this even clearer because they distinguish between `mirror` and `remote` workspace models, each with different tradeoffs for local-vs-remote canonical state; runtime design.

**So no, I am not moving away from OpenShell.**

I am giving OpenShell a better home.

## Full Design

![openclaw on proxmox](https://pbrazeale.github.io/images/openclaw-on-proxmox_20260405.webp)
So the stack now becomes much easier to describe:

- **Proxmox** hosts the lab
- **VMs** separate concerns
- **Docker** and **Portainer** run the services
- **OpenShell** remains the controlled execution boundary
- **OpenClaw** is the agent runtime layer
- **Browser** and **MCPs** get their own isolated spaces

## Agent Swarms

This matters even more once the goal shifts from “my assistant works” to “my agent ecosystem is growing.”

A swarm is not just more prompts.

It's more trust boundaries, more tool permissions, more workspace rules, more failure modes, more paths for accidental access, and more opportunities for one experiment to poison another **if you have not separated the environments properly**.

Swarm design **is** infrastructure design.

That is the real lesson I’ve taken from the last couple of weeks. The exciting part is still the agents, yes. **But the leverage increasingly comes from the operating model around them.**

That is the same story showing up all over software right now: when one person can attempt more, the systems around that person matter more too.

## Building Now

So, for my part, this is the path forward:

- Stand up **Proxmox** as the durable lab host on the new **HP Z8**
- Keep stable services separate from dangerous experiments
- Use **Docker** as the packaging layer for replaceable deployment
  - Use **Portainer** as my management plane; same as I use the proxmox web portal. Or how I built NovelFoundry on Dokploy. [NovelFoundry Dokploy](https://pbrazeale.github.io/posts/dev-week-073/#backend)
- Keep **OpenShell** in the stack, but let it do the job it's actually designed to do, and drop **NemoClaw**.
- And start treating browser tooling, MCP workflows, and swarm experiments like real infrastructure concerns instead of clever laptop tricks.

The ThinkPad phase was not a mistake. It was the proof.

**This is the build that comes after proof.**

## Sources

[1]: https://pbrazeale.github.io/posts/nemoclaw-setup/
[2]: https://docs.openclaw.ai/gateway/openshell
[3]: https://docs.openclaw.ai/gateway/security
[4]: https://pbrazeale.github.io/posts/vibe-coding-01/
[5]: https://www.proxmox.com/en/products/proxmox-virtual-environment/overview
[6]: https://pve.proxmox.com/wiki/Live_Snapshots
[7]: https://docs.docker.com/engine/install/debian/
[8]: https://docs.portainer.io/start/install-ce/server/docker/linux

## Tags

[[50 IT]] [[59.07 Proxmox + OpenClaw Issue 2026-04-04]]

[[openclaw]] [[linux]] [[Proxmox]] [[docker]] [[nemoclaw]] [[openshell]]
