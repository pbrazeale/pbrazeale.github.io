+++
tags = ['Home Lab', 'Virtual Environment', 'Linux', 'Articles', 'TrueNAS', 'Proxmox']
title = 'TrueNas to Proxmox to LXC'
date = 2025-04-14T22:01:07+01:00
draft = false
+++

## Setting Up Jellyfin in an LXC on Proxmox

To save time, I highly recommend using this [community helper script](https://community-scripts.github.io/ProxmoxVE/scripts?id=jellyfin) to install Jellyfin. It shaved off 30 minutes compared to my first setup.

### Mount a TrueNAS Shared Folder to Your Jellyfin LXC

1. **Access your Proxmox node's shell.**

2. **Create a mount point for your shared media folder:**

   ```bash
   mkdir /mnt/media
   ```

3. **Install `cifs-utils` to enable SMB/CIFS mounting:**

   ```bash
   apt-get install cifs-utils
   ```

4. **Mount your TrueNAS shared folder to `/mnt/media`:**

   ```bash
   mount -t cifs -o user=<yourUsername> //<TrueNAS_IP>/<SharedFolderName> /mnt/media
   ```

   - Replace `<yourUsername>`, `<TrueNAS_IP>`, and `<SharedFolderName>` accordingly.
   - Example: `mount -t cifs -o user=john //<192.168.1.100>/media /mnt/media`

5. **Enter your password when prompted.**

6. **Bind the mounted directory to your LXC container:**

   ```bash
   pct set <LXC_ID> -mp0 /mnt/media,mp=/shared
   ```

   - Replace `<LXC_ID>` with the ID of your Jellyfin container.

7. **Reboot the LXC container:**

   ```bash
   pct reboot <LXC_ID>
   ```

8. **Log into Jellyfin.**
   - When adding a media folder, you should now see `/shared` available.
