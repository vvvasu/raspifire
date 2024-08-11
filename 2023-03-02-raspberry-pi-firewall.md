---
title: Raspberry Pi Firewall
author: Vishwa Vasu
---

This blog is based on my project for my bachelor&#8217;s degree back in 2019.

The solution I will present to you is good for the people who value their information to be protected(home users) and small-scale businesses.

Before it begins, let&#8217;s look at what a firewall is**.**

<blockquote class="wp-block-quote is-layout-flow wp-block-quote-is-layout-flow">
  <p>
    According to the CISCO, a firewall is a network security device that monitors incoming and outgoing traffic and determines whether to allow or deny that particular traffic according to the defined set of firewall rules
  </p>
  
  <cite>&#8220;<a href="https://www.cisco.com/c/en/us/products/security/firewalls/what-is-a-firewall.html" data-type="URL" data-id="https://www.cisco.com/c/en/us/products/security/firewalls/what-is-a-firewall.html" target="_blank" rel="noreferrer noopener">Cisco</a>&#8220;</cite>
</blockquote>

There are different kinds of firewalls. It can be a hardware, software or cloud firewall.

## IPFire Firewall

IPFire is an open-source firewall, and it&#8217;s freely available. It gives freedom to modify the source code and configuration files. It is developed under the Linux distribution. It is based on stateful packet filtering and offers various features.

IPFire has a configurable web dashboard to control firewall features. A firewall is a router. Therefore, the IPFire can also act as a router, with features such as DHCP and a DNS server. IPFire firewall can be configured as a wireless access point, and its VPN settings configurable firewall for safe and encrypted connection over a secure network.

IPFire has a package manager called &#8220;Pakfire&#8221;, and we can add add-ons such as Hostapd, watchdog, guardian, Who Is Online (WIO), etc…

## Why Raspberry-pi?

Raspberry Pi 3 b+ mini-computer can be used as the hardware component for the solution. Raspberry Pi has features required to build the IPFire firewall. A Broadcom BCM2887B0 processor powers it with an ARMv8 64-bit 1.4 GHz system on a chip. It has 1 GB LPDDR2 SDRAM and two network interfaces, which are 2.4GHz IEEE 802.11.b/g/n/ac Wireless LAN with 4.0 Bluetooth and a Gigabit Ethernet over USB 2.0 with a maximum throughput of 300 Mbps. It uses low electricity because it has a 5V/2.5A power input. It supports Power over Ethernet.

Raspberry Pi is a multipurpose, low-cost, and advanced mini-computer. It is small in scale as a credit card size. It supports Linux-based OSes. IPFIRE has been written in Linux since version 2. It only needs 1GHz of CPU, 512MB of RAM and 4GB memory storage. As a firewall needs inbound and outbound network interfaces, Raspberry Pi can supply that by wireless LAN and the Gigabit ethernet over USB 2.0

Raspberry Pi does not have a real-time clock because it doesn&#8217;t have a backup battery. But IPFire has a Network Time Sensor to provide that facility.

## Requirements

#### Hardware

<ul class="wp-block-list">
  <li>
    PC
  </li>
  <li>
    SD Card &#8211; 8GB
  </li>
  <li>
    Raspberry Pi 3b+ or higher version
  </li>
  <li>
    External Monitor
  </li>
  <li>
    HDMI Cable
  </li>
  <li>
    Wired Mouse, Keyboard
  </li>
  <li>
    2 Ethernet Cables
  </li>
  <li>
    USB to Ethernet adapter
  </li>
  <li>
    Home Router
  </li>
  <li>
    Router for outgoing connections
  </li>
</ul>

#### Software

<ul class="wp-block-list">
  <li>
    <a href="https://downloads.ipfire.org/releases/ipfire-2.x/2.27-core170/ipfire-2.27-core170-armv6l.img.xz">ipfire-2.27.2gb-ext4.armv6l-full-core167.img</a>
  </li>
  <li>
    <a href="https://downloads.raspberrypi.org/imager/imager_latest.exe" data-type="URL" data-id="https://downloads.raspberrypi.org/imager/imager_latest.exe" target="_blank" rel="noreferrer noopener">Raspberry Pi imager</a>
  </li>
</ul>

## Network Architecture

<img loading="lazy" decoding="async" width="711" height="441" src="https://vazdefense.com/wp-content/uploads/2022/10/Network-Setup.png" alt="Network Setup" class="wp-image-282" srcset="https://vazdefense.com/wp-content/uploads/2022/10/Network-Setup.png 711w, https://vazdefense.com/wp-content/uploads/2022/10/Network-Setup-300x186.png 300w" sizes="(max-width: 711px) 100vw, 711px" /> </figure> 

## Installation Process

Download the latest IPFire ARM image and boot it into the SD Card using Raspberry Pi Imager.

The ARM flash image is configured for the serial console by default. Therefore, the IPFire firewall&#8217;s image configuration files must be modified before booting up the firewall.

Since we are using HDMI & USB Keyboard, edit the uENV.txt file and change SERIAL-CONSOLE=ON to OFF, as shown in the image.<figure class="wp-block-image size-full">

<img loading="lazy" decoding="async" width="852" height="801" src="https://vazdefense.com/wp-content/uploads/2022/10/Modified-configurations.png" alt="" class="wp-image-266" srcset="https://vazdefense.com/wp-content/uploads/2022/10/Modified-configurations.png 852w, https://vazdefense.com/wp-content/uploads/2022/10/Modified-configurations-300x282.png 300w, https://vazdefense.com/wp-content/uploads/2022/10/Modified-configurations-768x722.png 768w" sizes="(max-width: 852px) 100vw, 852px" /> </figure> <figure class="wp-block-image size-full"><img loading="lazy" decoding="async" width="998" height="381" src="https://vazdefense.com/wp-content/uploads/2022/10/Serial-console-change.png" alt="" class="wp-image-320" srcset="https://vazdefense.com/wp-content/uploads/2022/10/Serial-console-change.png 998w, https://vazdefense.com/wp-content/uploads/2022/10/Serial-console-change-300x115.png 300w, https://vazdefense.com/wp-content/uploads/2022/10/Serial-console-change-768x293.png 768w" sizes="(max-width: 998px) 100vw, 998px" /><figcaption class="wp-element-caption">_uEnv.txt file configuratio_n</figcaption></figure> 

## Configuration Steps

Insert the SD card into the Raspberry Pi. Prepare an external router to use as an access point with the green interface. Connect that router to the desired network port, which will be used as a green interface. The red interface should connect to the incoming connection. Our incoming source is the home router. Connect Raspberry Pi&#8217;s desired red interface port to the home router and power the Raspberry Pi on. We have to use an external monitor for the first time to configure the basics.

After first booting up, you will get the following screen:<figure class="wp-block-image size-full">

<img loading="lazy" decoding="async" width="982" height="722" src="https://vazdefense.com/wp-content/uploads/2022/10/Keeyboard-mapping.png" alt="" class="wp-image-285" srcset="https://vazdefense.com/wp-content/uploads/2022/10/Keeyboard-mapping.png 982w, https://vazdefense.com/wp-content/uploads/2022/10/Keeyboard-mapping-300x221.png 300w, https://vazdefense.com/wp-content/uploads/2022/10/Keeyboard-mapping-768x565.png 768w" sizes="(max-width: 982px) 100vw, 982px" /> </figure> 

### Keyboard Mapping

The first setup is the Keyboard layout. Select your desired keyboard setup and continue.<figure class="wp-block-image size-full">

<img loading="lazy" decoding="async" width="1011" height="722" src="https://vazdefense.com/wp-content/uploads/2022/10/Keyboard-Layout.png" alt="" class="wp-image-286" srcset="https://vazdefense.com/wp-content/uploads/2022/10/Keyboard-Layout.png 1011w, https://vazdefense.com/wp-content/uploads/2022/10/Keyboard-Layout-300x214.png 300w, https://vazdefense.com/wp-content/uploads/2022/10/Keyboard-Layout-768x548.png 768w" sizes="(max-width: 1011px) 100vw, 1011px" /> </figure> 

### Timezone

The next setup is time zone. I use my current location&#8217;s time zone.<figure class="wp-block-image size-full">

<img loading="lazy" decoding="async" width="955" height="722" src="https://vazdefense.com/wp-content/uploads/2022/10/Timezone-Berlin.png" alt="" class="wp-image-287" srcset="https://vazdefense.com/wp-content/uploads/2022/10/Timezone-Berlin.png 955w, https://vazdefense.com/wp-content/uploads/2022/10/Timezone-Berlin-300x227.png 300w, https://vazdefense.com/wp-content/uploads/2022/10/Timezone-Berlin-768x581.png 768w" sizes="(max-width: 955px) 100vw, 955px" /> </figure> 

### Hostname

Next is the hostname. Use a hostname as you desire, or continue with defaults.<figure class="wp-block-image size-full">

<img loading="lazy" decoding="async" width="917" height="722" src="https://vazdefense.com/wp-content/uploads/2022/10/hostname-conf.png" alt="" class="wp-image-289" srcset="https://vazdefense.com/wp-content/uploads/2022/10/hostname-conf.png 917w, https://vazdefense.com/wp-content/uploads/2022/10/hostname-conf-300x236.png 300w, https://vazdefense.com/wp-content/uploads/2022/10/hostname-conf-768x605.png 768w" sizes="(max-width: 917px) 100vw, 917px" /> </figure> 

### Domain Name

The following setup is the domain name. I will continue with defaults.<figure class="wp-block-image size-full">

<img loading="lazy" decoding="async" width="932" height="722" src="https://vazdefense.com/wp-content/uploads/2022/10/domain-name-conf.png" alt="" class="wp-image-290" srcset="https://vazdefense.com/wp-content/uploads/2022/10/domain-name-conf.png 932w, https://vazdefense.com/wp-content/uploads/2022/10/domain-name-conf-300x232.png 300w, https://vazdefense.com/wp-content/uploads/2022/10/domain-name-conf-768x595.png 768w" sizes="(max-width: 932px) 100vw, 932px" /> </figure> 

### Networking

These steps are the most critical setups in the firewall. Here, we have to configure the network configuration type, driver&#8217;s card assignment, and address settings.<figure class="wp-block-image size-full">

<img loading="lazy" decoding="async" width="927" height="721" src="https://vazdefense.com/wp-content/uploads/2022/10/Networking-setup.png" alt="" class="wp-image-291" srcset="https://vazdefense.com/wp-content/uploads/2022/10/Networking-setup.png 927w, https://vazdefense.com/wp-content/uploads/2022/10/Networking-setup-300x233.png 300w, https://vazdefense.com/wp-content/uploads/2022/10/Networking-setup-768x597.png 768w" sizes="(max-width: 927px) 100vw, 927px" /> </figure> 

### Network configuration type

In this setup, I will use three interfaces (Red+Green+Blue). As I mentioned earlier, Red is used for incoming communications. Green and Blue are for outgoing communications in my setup.<figure class="wp-block-image size-full">

<img loading="lazy" decoding="async" width="1007" height="723" src="https://vazdefense.com/wp-content/uploads/2022/10/Interfaces-assignment.png" alt="" class="wp-image-292" srcset="https://vazdefense.com/wp-content/uploads/2022/10/Interfaces-assignment.png 1007w, https://vazdefense.com/wp-content/uploads/2022/10/Interfaces-assignment-300x215.png 300w, https://vazdefense.com/wp-content/uploads/2022/10/Interfaces-assignment-768x551.png 768w" sizes="(max-width: 1007px) 100vw, 1007px" /> </figure> 

### Drivers and card assignments

Raspberry Pi has two built-in network cards. I have used one extra network card with a USB to Ethernet network adapter.

I use network cards in my setup, as shown in the following image.<figure class="wp-block-image size-full">

<img loading="lazy" decoding="async" width="1001" height="722" src="https://vazdefense.com/wp-content/uploads/2022/10/Network-card-assignment.png" alt="" class="wp-image-293" srcset="https://vazdefense.com/wp-content/uploads/2022/10/Network-card-assignment.png 1001w, https://vazdefense.com/wp-content/uploads/2022/10/Network-card-assignment-300x216.png 300w, https://vazdefense.com/wp-content/uploads/2022/10/Network-card-assignment-768x554.png 768w" sizes="(max-width: 1001px) 100vw, 1001px" /> </figure> 

### Address settings

I will configure the Red interface&#8217;s IP address to get an IP from the home router&#8217;s DHCP pool. Green interface as 10.10.10.1/24 and Blue interface as 10.20.20.1/24.<figure class="wp-block-image size-full">

<img loading="lazy" decoding="async" width="922" height="723" src="https://vazdefense.com/wp-content/uploads/2022/10/IP-add-config-for-RED.png" alt="" class="wp-image-294" srcset="https://vazdefense.com/wp-content/uploads/2022/10/IP-add-config-for-RED.png 922w, https://vazdefense.com/wp-content/uploads/2022/10/IP-add-config-for-RED-300x235.png 300w, https://vazdefense.com/wp-content/uploads/2022/10/IP-add-config-for-RED-768x602.png 768w" sizes="(max-width: 922px) 100vw, 922px" /> <figcaption class="wp-element-caption">_Interface Red IP address setting_</figcaption></figure> <figure class="wp-block-image size-full"><img loading="lazy" decoding="async" width="902" height="720" src="https://vazdefense.com/wp-content/uploads/2022/10/IP-add-config-for-Green.png" alt="" class="wp-image-295" srcset="https://vazdefense.com/wp-content/uploads/2022/10/IP-add-config-for-Green.png 902w, https://vazdefense.com/wp-content/uploads/2022/10/IP-add-config-for-Green-300x239.png 300w, https://vazdefense.com/wp-content/uploads/2022/10/IP-add-config-for-Green-768x613.png 768w" sizes="(max-width: 902px) 100vw, 902px" /><figcaption class="wp-element-caption">_Interface Green IP address setting_</figcaption></figure> <figure class="wp-block-image size-full"><img loading="lazy" decoding="async" width="957" height="723" src="https://vazdefense.com/wp-content/uploads/2022/10/Int-blue-configuration.png" alt="" class="wp-image-296" srcset="https://vazdefense.com/wp-content/uploads/2022/10/Int-blue-configuration.png 957w, https://vazdefense.com/wp-content/uploads/2022/10/Int-blue-configuration-300x227.png 300w, https://vazdefense.com/wp-content/uploads/2022/10/Int-blue-configuration-768x580.png 768w" sizes="(max-width: 957px) 100vw, 957px" /><figcaption class="wp-element-caption">_Interface Blue IP address setting_</figcaption></figure> 

After this window, you will see the DHCP setup for green and blue. Configure the DHCP range as you desire. I will use Google&#8217;s DNS for the secondary DNS. (This setup is not showing in the image. You can change this setting in anytime from the web interface)

### Root and Admin Passwords

The next step is to set up the root password and admin password. You have to use the root password to connect to the firewall in the command line setup or when using SSH to connect to the firewall. The admin password is for the web configurator setup in IPFire&#8217;s web interface.

Now, the setup is complete. The firewall will reboot; you can see the configured settings when booting.

Connect to the configured green interface using the access point.  
Access the web configurator using interface IP addresses. For the first time setup, I used the green interface&#8217;s IP to log in to the firewall&#8217;s web interfaces. IPFire has the default port number&#8217; 444&#8242; for the web interface.

Use the admin username and password to log in.<figure class="wp-block-image size-full">

<img loading="lazy" decoding="async" width="1486" height="760" src="https://vazdefense.com/wp-content/uploads/2022/10/web-configurator-login.png" alt="" class="wp-image-297" srcset="https://vazdefense.com/wp-content/uploads/2022/10/web-configurator-login.png 1486w, https://vazdefense.com/wp-content/uploads/2022/10/web-configurator-login-300x153.png 300w, https://vazdefense.com/wp-content/uploads/2022/10/web-configurator-login-1024x524.png 1024w, https://vazdefense.com/wp-content/uploads/2022/10/web-configurator-login-768x393.png 768w" sizes="(max-width: 1486px) 100vw, 1486px" /> <figcaption class="wp-element-caption">_IPFire web interface login_</figcaption></figure> 

You can see the home screen with the configured interfaces.

### IPFire Web Interface

You can see the home screen with the configured interfaces.<figure class="wp-block-image size-full">

<img loading="lazy" decoding="async" width="1291" height="542" src="https://vazdefense.com/wp-content/uploads/2022/10/main-page.png" alt="" class="wp-image-298" srcset="https://vazdefense.com/wp-content/uploads/2022/10/main-page.png 1291w, https://vazdefense.com/wp-content/uploads/2022/10/main-page-300x126.png 300w, https://vazdefense.com/wp-content/uploads/2022/10/main-page-1024x430.png 1024w, https://vazdefense.com/wp-content/uploads/2022/10/main-page-768x322.png 768w" sizes="(max-width: 1291px) 100vw, 1291px" /> </figure> 

### Blue Interface Setup, hostapd

We assigned a network card for the blue interface earlier. But to activate it, we have to install the &#8220;hostapd&#8221; add-on. You can install it using &#8220;Pakfire&#8221;.<figure class="wp-block-image size-full">

<img loading="lazy" decoding="async" width="1253" height="711" src="https://vazdefense.com/wp-content/uploads/2022/10/Installed-hostapd.png" alt="" class="wp-image-300" srcset="https://vazdefense.com/wp-content/uploads/2022/10/Installed-hostapd.png 1253w, https://vazdefense.com/wp-content/uploads/2022/10/Installed-hostapd-300x170.png 300w, https://vazdefense.com/wp-content/uploads/2022/10/Installed-hostapd-1024x581.png 1024w, https://vazdefense.com/wp-content/uploads/2022/10/Installed-hostapd-768x436.png 768w" sizes="(max-width: 1253px) 100vw, 1253px" /> </figure> 

After the installation, you will see a new add-on page called &#8220;WLAN AP&#8221; under the &#8220;Pakfire&#8221;. Configure the settings as follows and activate the Blue interface&#8217;s access point.<figure class="wp-block-image size-full">

<img loading="lazy" decoding="async" width="1276" height="842" src="https://vazdefense.com/wp-content/uploads/2022/10/Wlan-AP-configuration.png" alt="" class="wp-image-301" srcset="https://vazdefense.com/wp-content/uploads/2022/10/Wlan-AP-configuration.png 1276w, https://vazdefense.com/wp-content/uploads/2022/10/Wlan-AP-configuration-300x198.png 300w, https://vazdefense.com/wp-content/uploads/2022/10/Wlan-AP-configuration-1024x676.png 1024w, https://vazdefense.com/wp-content/uploads/2022/10/Wlan-AP-configuration-768x507.png 768w" sizes="(max-width: 1276px) 100vw, 1276px" /> </figure> 

Now you will see both access points as follows in available wifi connections.<figure class="wp-block-image size-full">

<img loading="lazy" decoding="async" width="217" height="105" src="https://vazdefense.com/wp-content/uploads/2022/10/Wifi-connections-from-ipfire.png" alt="" class="wp-image-302" /> </figure> 

### IPFire&#8217;s default firewall behaviour

By default, IPFire allows in and out connections. You can change it by setting the following as &#8220;Blocked&#8221;.<figure class="wp-block-image size-full">

<img loading="lazy" decoding="async" width="1211" height="302" src="https://vazdefense.com/wp-content/uploads/2022/10/Default-behaviour-of-firewall.png" alt="" class="wp-image-303" srcset="https://vazdefense.com/wp-content/uploads/2022/10/Default-behaviour-of-firewall.png 1211w, https://vazdefense.com/wp-content/uploads/2022/10/Default-behaviour-of-firewall-300x75.png 300w, https://vazdefense.com/wp-content/uploads/2022/10/Default-behaviour-of-firewall-1024x255.png 1024w, https://vazdefense.com/wp-content/uploads/2022/10/Default-behaviour-of-firewall-768x192.png 768w" sizes="(max-width: 1211px) 100vw, 1211px" /> </figure> 

#### SSH access to the firewall

Configure the SSH settings as follows. After this, you can set up your Raspberry Pi anywhere and log in with root access to configure it in the terminal.<figure class="wp-block-image size-full">

<img loading="lazy" decoding="async" width="1286" height="556" src="https://vazdefense.com/wp-content/uploads/2022/10/SSH-configuration-1.png" alt="" class="wp-image-304" srcset="https://vazdefense.com/wp-content/uploads/2022/10/SSH-configuration-1.png 1286w, https://vazdefense.com/wp-content/uploads/2022/10/SSH-configuration-1-300x130.png 300w, https://vazdefense.com/wp-content/uploads/2022/10/SSH-configuration-1-1024x443.png 1024w, https://vazdefense.com/wp-content/uploads/2022/10/SSH-configuration-1-768x332.png 768w" sizes="(max-width: 1286px) 100vw, 1286px" /> </figure> 

SSH configuration from the web interface<figure class="wp-block-image size-full">

<img loading="lazy" decoding="async" width="1037" height="418" src="https://vazdefense.com/wp-content/uploads/2022/10/Interfaces-as-a-summary.png" alt="" class="wp-image-305" srcset="https://vazdefense.com/wp-content/uploads/2022/10/Interfaces-as-a-summary.png 1037w, https://vazdefense.com/wp-content/uploads/2022/10/Interfaces-as-a-summary-300x121.png 300w, https://vazdefense.com/wp-content/uploads/2022/10/Interfaces-as-a-summary-1024x413.png 1024w, https://vazdefense.com/wp-content/uploads/2022/10/Interfaces-as-a-summary-768x310.png 768w" sizes="(max-width: 1037px) 100vw, 1037px" /> <figcaption class="wp-element-caption">_SSH login from PC_</figcaption></figure> 

Now, the firewall is up and running. We can test it by configuring some firewall rules.

## Testing

### Firewall rules

Firewall rules work with the top-to-bottom lineup. I have configured some of the basic firewall rules to test it.<figure class="wp-block-image size-full">

<img loading="lazy" decoding="async" width="1250" height="557" src="https://vazdefense.com/wp-content/uploads/2022/10/Firewall-rules.png" alt="" class="wp-image-308" srcset="https://vazdefense.com/wp-content/uploads/2022/10/Firewall-rules.png 1250w, https://vazdefense.com/wp-content/uploads/2022/10/Firewall-rules-300x134.png 300w, https://vazdefense.com/wp-content/uploads/2022/10/Firewall-rules-1024x456.png 1024w, https://vazdefense.com/wp-content/uploads/2022/10/Firewall-rules-768x342.png 768w" sizes="(max-width: 1250px) 100vw, 1250px" /> </figure> 

The first firewall rule is to deny SSH access from 10.20.20.4 pc in the Blue interface to 10.10.10.3 pc in the Green interface. It will give a timeout error since the rule is to deny the connections.<figure class="wp-block-image size-full">

<img loading="lazy" decoding="async" width="708" height="255" src="https://vazdefense.com/wp-content/uploads/2022/10/SSH-from-kali@kali.png" alt="" class="wp-image-309" srcset="https://vazdefense.com/wp-content/uploads/2022/10/SSH-from-kali@kali.png 708w, https://vazdefense.com/wp-content/uploads/2022/10/SSH-from-kali@kali-300x108.png 300w" sizes="(max-width: 708px) 100vw, 708px" /> </figure> 

The next two firewall rules are to test the telnet access by blocking the 1337 port from 10.10.10.3 to 10.20.20.4 and allowing telnet access with the 1667 port from 10.10.10.3 to 10.20.20.4. 2nd rule denies access, and 3rd rule provides access, as in the following images.<figure class="wp-block-image size-full">

<img loading="lazy" decoding="async" width="772" height="416" src="https://vazdefense.com/wp-content/uploads/2022/10/Telnet-from-vasu@kali.png" alt="" class="wp-image-310" srcset="https://vazdefense.com/wp-content/uploads/2022/10/Telnet-from-vasu@kali.png 772w, https://vazdefense.com/wp-content/uploads/2022/10/Telnet-from-vasu@kali-300x162.png 300w, https://vazdefense.com/wp-content/uploads/2022/10/Telnet-from-vasu@kali-768x414.png 768w" sizes="(max-width: 772px) 100vw, 772px" /> <figcaption class="wp-element-caption">_The result from the Green interface_</figcaption></figure> <figure class="wp-block-image size-full"><img loading="lazy" decoding="async" width="666" height="366" src="https://vazdefense.com/wp-content/uploads/2022/10/ping-from-kali@kali.png" alt="" class="wp-image-311" srcset="https://vazdefense.com/wp-content/uploads/2022/10/ping-from-kali@kali.png 666w, https://vazdefense.com/wp-content/uploads/2022/10/ping-from-kali@kali-300x165.png 300w" sizes="(max-width: 666px) 100vw, 666px" /><figcaption class="wp-element-caption">_The results from the Blue interface_</figcaption></figure> 

Besides the above rules, a firewall allows access to any connections between interfaces.<figure class="wp-block-image size-full">

<img loading="lazy" decoding="async" width="666" height="366" src="https://vazdefense.com/wp-content/uploads/2022/10/ping-from-kali@kali-1.png" alt="" class="wp-image-312" srcset="https://vazdefense.com/wp-content/uploads/2022/10/ping-from-kali@kali-1.png 666w, https://vazdefense.com/wp-content/uploads/2022/10/ping-from-kali@kali-1-300x165.png 300w" sizes="(max-width: 666px) 100vw, 666px" /> <figcaption class="wp-element-caption">_Ping probes to the Green interface from the Blue interface_</figcaption></figure> 

<p class="has-small-font-size">
  <strong>There are more blogs related to the Raspberry Pi firewall to come. Stay tuned 🙂 </strong>
</p>
