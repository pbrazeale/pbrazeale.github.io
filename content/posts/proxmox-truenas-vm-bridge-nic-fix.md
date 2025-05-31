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
