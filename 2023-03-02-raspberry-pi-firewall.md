
---
# Raspberry Pi Firewall
*vasu@vdefense.tech*
---

This blog is based on my project for my bachelor's degree back in 2019.

The solution I present here is ideal for individuals who value their information security (home users) and small-scale businesses.

Before we begin, let's look at what a firewall is.

> According to Cisco, a firewall is a network security device that monitors incoming and outgoing traffic and determines whether to allow or deny that particular traffic based on a defined set of firewall rules.
> 
> — [Cisco](https://www.cisco.com/c/en/us/products/security/firewalls/what-is-a-firewall.html)

There are different kinds of firewalls: hardware, software, or cloud-based.

## IPFire Firewall

IPFire is an open-source firewall, freely available and customizable. It is developed under the Linux distribution and is based on stateful packet filtering, offering various features.

IPFire has a configurable web dashboard to control firewall features. Since a firewall is a type of router, IPFire can also act as a router with features such as DHCP and a DNS server. IPFire can be configured as a wireless access point, and its VPN settings can provide a secure and encrypted connection over a secure network.

IPFire has a package manager called "Pakfire," which allows us to add add-ons such as Hostapd, watchdog, guardian, Who Is Online (WIO), and more.

## Why Raspberry Pi?

The Raspberry Pi 3 B+ mini-computer can be used as the hardware component for this solution. It has the necessary features to build the IPFire firewall. Powered by a Broadcom BCM2837B0 processor with an ARMv8 64-bit 1.4 GHz system on a chip, it has 1 GB of LPDDR2 SDRAM and two network interfaces: 2.4GHz IEEE 802.11.b/g/n/ac Wireless LAN with Bluetooth 4.0 and a Gigabit Ethernet over USB 2.0 with a maximum throughput of 300 Mbps. It consumes low power, requiring only a 5V/2.5A power input, and supports Power over Ethernet (PoE).

Raspberry Pi is a multipurpose, low-cost, and advanced mini-computer, small in size like a credit card. It supports Linux-based operating systems. IPFire has been developed on Linux since version 2. It requires only a 1GHz CPU, 512MB RAM, and 4GB of memory storage. As a firewall needs inbound and outbound network interfaces, the Raspberry Pi provides that via wireless LAN and Gigabit Ethernet over USB 2.0.

Raspberry Pi does not have a real-time clock due to the absence of a backup battery, but IPFire includes a Network Time Sensor to provide this functionality.

## Requirements

### Hardware

- PC
- SD Card (8GB or larger)
- Raspberry Pi 3 B+ or higher
- External Monitor
- HDMI Cable
- Wired Mouse and Keyboard
- 2 Ethernet Cables
- USB to Ethernet adapter
- Home Router
- Router for outgoing connections

### Software

- [IPFire Image](https://downloads.ipfire.org/releases/ipfire-2.x/2.27-core170/ipfire-2.27-core170-armv6l.img.xz)
- [Raspberry Pi Imager](https://downloads.raspberrypi.org/imager/imager_latest.exe)

## Network Architecture

![Network Setup](https://github.com/vvvasu/raspifire/blob/main/Network-Setup.png)

## Installation Process

Download the latest IPFire ARM image and flash it to the SD Card using Raspberry Pi Imager.

The ARM flash image is configured for the serial console by default. Therefore, the IPFire firewall's image configuration files must be modified before booting up the firewall.

Since we are using HDMI and a USB Keyboard, edit the `uENV.txt` file and change `SERIAL-CONSOLE=ON` to `OFF`, as shown in the image below.

![Modified Configurations](https://vazdefense.com/wp-content/uploads/2022/10/Modified-configurations.png)

![Serial Console Change](https://vazdefense.com/wp-content/uploads/2022/10/Serial-console-change.png)

## Configuration Steps

Insert the SD card into the Raspberry Pi. Prepare an external router to use as an access point with the green interface. Connect that router to the desired network port, which will be used as a green interface. The red interface should connect to the incoming connection. Our incoming source is the home router. Connect the Raspberry Pi's desired red interface port to the home router and power on the Raspberry Pi. An external monitor is required for the initial configuration.

Upon the first boot, you will see the following screen:

![Keyboard Mapping](https://vazdefense.com/wp-content/uploads/2022/10/Keeyboard-mapping.png)

### Keyboard Mapping

The first setup is the Keyboard layout. Select your desired keyboard setup and continue.

![Keyboard Layout](https://vazdefense.com/wp-content/uploads/2022/10/Keyboard-Layout.png)

### Timezone

The next setup is the time zone. Use your current location's time zone.

![Timezone](https://vazdefense.com/wp-content/uploads/2022/10/Timezone-Berlin.png)

### Hostname

Next, set up the hostname. You can use a custom hostname or continue with the default.

![Hostname](https://vazdefense.com/wp-content/uploads/2022/10/hostname-conf.png)

### Domain Name

The next setup is the domain name. I will continue with the default settings.

![Domain Name](https://vazdefense.com/wp-content/uploads/2022/10/domain-name-conf.png)

### Networking

These steps involve the most critical setup in the firewall: configuring the network type, driver assignments, and address settings.

![Networking Setup](https://vazdefense.com/wp-content/uploads/2022/10/Networking-setup.png)

### Network Configuration Type

In this setup, I will use three interfaces (Red, Green, and Blue). As mentioned earlier, Red is used for incoming communications, while Green and Blue are for outgoing communications.

![Interfaces Assignment](https://vazdefense.com/wp-content/uploads/2022/10/Interfaces-assignment.png)

### Drivers and Card Assignments

The Raspberry Pi has two built-in network cards. I have used an additional network card with a USB to Ethernet network adapter.

I assigned the network cards as shown in the image below.

![Network Card Assignment](https://vazdefense.com/wp-content/uploads/2022/10/Network-card-assignment.png)

### Address Settings

I configured the Red interface's IP address to get an IP from the home router's DHCP pool. The Green interface is set as `10.10.10.1/24`, and the Blue interface as `10.20.20.1/24`.

![Red Interface IP Address Setting](https://vazdefense.com/wp-content/uploads/2022/10/IP-add-config-for-RED.png)

![Green Interface IP Address Setting](https://vazdefense.com/wp-content/uploads/2022/10/IP-add-config-for-Green.png)

![Blue Interface IP Address Setting](https://vazdefense.com/wp-content/uploads/2022/10/Int-blue-configuration.png)

After this, you will see the DHCP setup for the Green and Blue interfaces. Configure the DHCP range as desired. I use Google's DNS for the secondary DNS. (This setup is not shown in the image but can be changed anytime from the web interface.)

### Root and Admin Passwords

The next step is to set up the root and admin passwords. The root password is used for command-line setup or SSH connections to the firewall. The admin password is used for the web configurator in IPFire's web interface.

Once completed, the firewall will reboot, and you can see the configured settings on boot.

Connect to the configured green interface using the access point.  
Access the web configurator using the interface IP address. For the first-time setup, I used the green interface's IP to log in to the firewall's web interface. IPFire uses port `444` by default for the web interface.

Use the admin username and password to log in.

![IPFire Web Interface Login](https://vazdefense.com/wp-content/uploads/2022/10/web-configurator-login.png)

### IPFire Web Interface

You will see the home screen with the configured interfaces.

![IPFire Main Page](https://vazdefense.com/wp-content/uploads/2022/10/main-page.png)

### Blue Interface Setup: hostapd

We assigned a network card for the blue interface earlier. To activate it, we need to install the "hostapd" add-on. You can install it using "Pakfire."

![Installed hostapd](https://vazdefense.com/wp-content/uploads/2022/10/Installed-hostapd.png)

After installation, you will see a new add-on page called "WLAN AP" under "Pakfire." Configure the settings as follows and activate the Blue interface's access point.

![WLAN AP Configuration](https://vazdefense.com/wp-content/uploads/2022/10/Wlan-AP-configuration.png)

Now you will see both access points available in the Wi-Fi connections.

![Wi-Fi Connections from IPFire](https://vazdefense.com/wp-content/uploads/2022/10/Wifi-connections-from-ipfire.png)

### IPFire's Default Firewall Behavior

By default, IPFire allows incoming and outgoing connections. You can change this by setting it to "Blocked."

![Default Firewall Behavior](https://vazdefense.com/wp-content/uploads/2022/10/Default-behaviour-of-firewall.png)

### SSH Access to the Firewall

Configure the SSH settings as follows. After this, you can set up your Raspberry Pi anywhere and log in with root access to configure it in the terminal.

![SSH Configuration](https://vazdefense.com/wp-content/uploads/2022/10/SSH-configuration-1.png)

SSH configuration from the web interface.

![Interfaces Summary](https://vazdefense.com/wp-content/uploads/2022/10/Interfaces-as-a-summary.png)

Now, the firewall is up and running. We can test it by configuring some firewall rules.

## Testing

### Firewall Rules

Firewall rules work with a top-to-bottom lineup. I have configured some basic firewall rules to test it.

![Firewall Rules](https://vazdefense.com/wp-content/uploads/2022/10/Firewall-rules.png)

The first firewall rule denies SSH access from the `10.20.20.4` PC in the Blue interface to the `10.10.10.3` PC in the Green interface. This will result in a timeout error since the rule denies the connection.

![SSH Denied](https://vazdefense.com/wp-content/uploads/2022/10/SSH-from-kali@kali.png)

The next two firewall rules test telnet access by blocking port 1337 from `10.10.10.3` to `10.20.20.4` and allowing telnet access on port 1667 from `10.10.10.3` to `10.20.20.4`. The second rule denies access, while the third rule allows it, as shown in the following images.

![Telnet Denied](https://vazdefense.com/wp-content/uploads/2022/10/Telnet-from-vasu@kali.png)

![Ping from Blue Interface](https://vazdefense.com/wp-content/uploads/2022/10/ping-from-kali@kali.png)

In addition to the above rules, the firewall allows access to any connections between interfaces.

![Ping from Blue Interface](https://vazdefense.com/wp-content/uploads/2022/10/ping-from-kali@kali-1.png)

**There are more blogs related to the Raspberry Pi firewall to come. Stay tuned 🙂**
