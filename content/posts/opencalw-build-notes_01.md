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
