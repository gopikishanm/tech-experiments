# Initial Setup

I have got my mini pc and ready to experiment things. I am planning to setup local kubernetes cluster in private network and run it.

## Hardware Specifications

- Ryzen7 5850U 4.4GHz Processor
- 32GB DDR4 3200MHz
- 1 TB SSD

## Operating System

Initial I thought of using VMWare ESXi. After going through multiple blog posts and what's best suited for my hardware I decided on using [Proxmox].

The installation guide on proxmox was very simple. I used `Rufus` to build a bootable pendrive. Then attached the pendrive to mini pc. I had to configure the boot options to boot from usb drive. The next steps were straight forward. I had to click Next and continue the installation. The installation was complete in few minutes and machine booted fine. I was able to login using root account. A web Url was printed on the screen and we can use it connect to Graphic UI.

When I tried to connect to the url, I always received timeout. I checked if the IP address used is part of my host network and it was fine. I re-installed Proxmox multiple times selecting different network interfaces. Still there was no connectivity to web URL.

I went back to documentation. The last step during installation phase is network configuration. Initially, I selected whichever interface was shown in the UI and continued. 

I missed below statement

```
Network interfaces that are UP show a filled circle in front of their name in the drop down menu
```

When I checked my interfaces, none were up. So, I googled further and found that [Proxmox] needs to be connected to LAN. I used cable to connect my mini-pc and started installation again.
This time, on network configuration step, I could see a `green dot` in front of network interface like :green_circle:. I selected it and continued installation. The installation was successful.

When I tried to connect to endpoint `https:\\192.168.1.111:8006`, I could see [Proxmox] UI. My first step done.

[Proxmox]: https://www.proxmox.com/en/
