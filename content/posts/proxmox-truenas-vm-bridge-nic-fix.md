+++
tags = ['Home Lab', 'Virtual Environment', 'Linux', 'Articles', 'TrueNAS', 'Proxmox']
title = 'Proxmox TrueNAS VM Bridge and NIC fix'
date = 2025-05-31T16:01:07+01:00
draft = false
+++

## 🖥️ Use the TrueNAS SCALE Console (via Proxmox)

In **Proxmox Web UI → TrueNAS VM → Console**:

Use console select `8` for `Open Linux Shell`

Then run:

```bash
ip a
```

Look for an interface named **`ens18`**, **`enp0s3`**, **`vtnet0`**, etc.

If **no IP is assigned**, run:

```bash
systemctl restart networking
```

Then request DHCP manually:

```bash
dhclient ens18
```

> Replace `ens18` with your NIC if it’s different.

### Drawbacks!

Changes the IP address from the original. Mapped netwrok drives will have to be updated.

##### NOTES/EXTRA READING:

[https://linux.die.net/man/8/dhclient](https://linux.die.net/man/8/dhclient)

> The DHCP protocol allows a host to contact a central server which maintains a list of IP addresses which may be assigned on one or more subnets.

[https://en.wikipedia.org/wiki/Dynamic_Host_Configuration_Protocol](https://en.wikipedia.org/wiki/Dynamic_Host_Configuration_Protocol)

> When connected to the network, and periodically thereafter, a client requests a set of parameters from the server using DHCP.
