---
title: VMWare Pro Homelab | Metasploitable2 & Vulnhub
# date: 2024-01-11 19:37:42 -500
image: /assets/images/thumbnails/homelab/Homelab-setup-guide-metasploit-vulnhub.jpg
author: Ethan Epperson
categories: 
    - blog
layout: post
---

## Creating/Importing the Isolated Network VMs

We will need to do some preparatory work and create an Ubuntu server machine before we get to setting up DVWA itself in the next part. The Metasploitable2 and VulnHub VMs will be imported into VMWare pre-configured, so we will have to manually adjust the specifications for those machines. As I mentioned in the intro, there are a multitude of VMs to choose from on VulnHub. Feel free to make your own choice about which one you want to start with. You can always add more later. I will be starting with the 'Symfonos: 1' machine, a beginner level box. This machine will be using DVWA on Ubuntu server. Here are the recommended specifications and the DHCP allocation in the webConfigurator.

![DVWA Specifications](/assets/images/homelab/isolated-vms-setup/dvwa-spec.jpg)

![DVWA DHCP](/assets/images/homelab/isolated-vms-setup/dvwa-dhcp.jpg)

## Installing Ubuntu Server

Power on the machine and choose 'Try or Install Ubuntu Server' and you will be greeted with the Ubuntu installation wizard after a short time. Choose your language, keyboard, and the standard server installation options. When you get to 'Network Connections' you should see the IP/MAC if you did everything correctly in the webConfigurator. Click 'Done'. On the next page it asks us for a proxy, we aren't using one so skip this section. Accept the default settings on the archive mirror page. On both of the storage configuration pages leave them as is and hit 'Done'. When asked to wipe the disk, click 'Confirm'. On the next screen, we will be able to choose a server name, username, and password. Once you have them entered, click 'Done'. We will not be using the pro version, so skip this step. On the next page, we want to install SSH so make sure to enable it before clicking 'Done'. We will not be installing any snaps, so skip and click 'Done'. Finally, we can allow Ubuntu to install. Once its done, reboot the system. Don't forget to test connections and update.

![Ubuntu Setup Language](/assets/images/homelab/isolated-vms-setup/ubuntu-language.jpg)

![Ubuntu Setup Keyboard](/assets/images/homelab/isolated-vms-setup/ubuntu-keyboard.jpg)

![Ubuntu Setup Type](/assets/images/homelab/isolated-vms-setup/ubuntu-type.jpg)

![Ubuntu Setup Network](/assets/images/homelab/isolated-vms-setup/ubuntu-network.jpg)

![Ubuntu Setup Proxy](/assets/images/homelab/isolated-vms-setup/ubuntu-proxy.jpg)

![Ubuntu Setup Mirror](/assets/images/homelab/isolated-vms-setup/ubuntu-mirror.jpg)

![Ubuntu Setup Storage](/assets/images/homelab/isolated-vms-setup/ubuntu-storage.jpg)

![Ubuntu Setup Storage Confirmation](/assets/images/homelab/isolated-vms-setup/ubuntu-storage2.jpg)

![Ubuntu Setup Profile](/assets/images/homelab/isolated-vms-setup/ubuntu-profile.jpg)

![Ubuntu Setup Pro](/assets/images/homelab/isolated-vms-setup/ubuntu-pro.jpg)

![Ubuntu Setup SSH](/assets/images/homelab/isolated-vms-setup/ubuntu-pro.jpg)

![Ubuntu Setup Snaps](/assets/images/homelab/isolated-vms-setup/ubuntu-snaps.jpg)

![Ubuntu Setup Installing](/assets/images/homelab/isolated-vms-setup/ubuntu-installing.jpg)

## Importing & Upgrading Metasploitable2 VM

To import Metasploitable2 into VMWare, ctrl-x and paste the unzipped metasploitable2 folder into the directory where all your virtual machines are stored. Once that's done, go to 'File' &rarr; 'Scan for Virtual Machines'. Make sure that Metasploitable is the box that is clicked. Follow the wizard and VMWare should register the metasploitable machine at this point. 

![Metasploitable2 Scan](/assets/images/homelab/isolated-vms-setup/meta-scan.jpg)

It should now show up under the library pane of VMware. Now we will need to reconfigure the hardware settings. Click on the VM and you should see the option 'Upgrade this virtual machine', choose it. The 'Change Hardware Compatibility Wizard' will be launched. On the wizard click through and choose the newest workstation version from the dropdown. On the next screen, choose 'Alter this virtual machine'. On the 'Review Changes' screen, click 'Finish' to convert and upgrade the virtual machine for use with Workstation X.X.X (17.5.x for the most current version at this time). 

![Metasploitable2 Hardware](/assets/images/homelab/isolated-vms-setup/meta-hardware.jpg)

![Metasploitable2 Workstation Compatibility](/assets/images/homelab/isolated-vms-setup/meta-compatibility.jpg)

![Metasploitable2 Review Changes](/assets/images/homelab/isolated-vms-setup/meta-changes.jpg)

![Metasploitable2 Finished Upgrading](/assets/images/homelab/isolated-vms-setup/meta-finished.jpg)

# Changing Metasploitable2 Settings

Now that we have upgraded the machine, we can change the specifications and set it's DHCP allocation. Luckily, the OS comes pre-installed so we don't have to worry about that. Here are recommended specs and the DHCP allocation within the webConfigurator.

![Metasploitable2 Specifications](/assets/images/homelab/isolated-vms-setup/meta-spec.jpg)

![Metasploitable2 DHCP](/assets/images/homelab/isolated-vms-setup/meta-dhcp.jpg)

Next, we can boot up our Metasploitable VM, login with the default credentials, and do the regular connection check. Let's start with a simple 'ifconfig -a' command. As we can see, the machine has the IP/MAC we set for it. 

![Metasploitable2 ifconfig Command](/assets/images/homelab/isolated-vms-setup/meta-ifconfig.jpg)

Now we absolutely do not want this machine to be able to have outbound access to other networks or the internet. Let's try our nslookup and curl commands once again and make sure that it fails. If it fails, then we have successfully blocked outbound traffic from this machine. If it doesn't, then your firewall rules are not configured correctly and you must change them ASAP. With that, metasploitable2 is done setting up.

## Importing and Upgrading the Symfonos: 1 VM

Importing the symphonos machine works a lot like metasploitable2, but instead of using the scan wizard to find metasploitable2 we will have to manually select it by going to 'File' &rarr; 'Open' and choosing the .ova file from the symfonos directory. The 'Import Virtual Machine Wizard' will launch and allow us to name it and choose an installation directory. 

![Symfonos: 1 Import](/assets/images/homelab/isolated-vms-setup/symfonos-import.jpg)

Here are the specifications and DHCP allocation in the webConfigurator.

![Symfonos: 1 Settings](/assets/images/homelab/isolated-vms-setup/symfonos-spec.jpg)

![Symfonos: 1 DHCP](/assets/images/homelab/isolated-vms-setup/vuln-dhcp.jpg)

We don't need to boot this machine right now as we don't have the login credentials. The point is to break into it and achieve root access. Be sure to double check your DHCP and firewall rules for OPT1 to make sure everything is in working order.

Once this is complete, then congrats all of the machines in our isolated network are now setup! We will be installing the DVWA web server onto Ubuntu here shortly. You can find the next part, 'VMWare Pro Homelab | DVWA', in the [blog] section of this site.