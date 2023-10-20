Insert tidligere modul her

---
## IOS Navigation

>All network devices requires an OS(Operating System) and that they can be configured using tools such as CLI or GUI.

### Primary Command Modes
Cisco IOS software separates the the management access into two command modes:
- User EXEC mode:
	- A mode with limited capabilities, but is still useful for basic operations.
	- It mostly consist of a limited number of monitoring commands.
	- Does not allow the execution of any commands that might change how the device is configured.
	- The user EXEC mode is identified by the CLI prompt that ends with the '>' symbol.
	- often referred to as "view-only" mode.
- Privileged EXEC mode:
	- For a user/network administrator to execute configuration commands, privileged EXEC mode is required and needs to be accessed.
	- Higher configuration modes such as global configuration mode, can only be reached/accessed by privileged EXEC mode. 
	- The mode can be identified by the prompt ending with the '#' symbol

### Configure Mode and Sub-configuration Modes
For a network administrator/user to configure the device, the global configuration mode needs to be accessed. 
- also commonly called ***global config mode***.

From Global Config Mode, CLI configuration changes are made that affects the operation of the devices as a whole.

> Global config mode is identified by a prompt that ends with '(config)#' after the device name, e.g., ***Austnes(config)#***. 

To access more and other specific configuration modes, we first have to enter global config mode. From there a user can enter different sub-configuration modes.
- Each of these modes allows the configuration of a particular part of function of the IOS device.  
Two common sub-config modes are:
- **Line Configuration Mode**: Used to configure console, [[Application Layer#SSH (Secure Shell)|SSH]], [[Application Layer#Telnet|Telnet]], or AUX access.
- **Interface Configuration Mode**: Used to configure a switch port or a router network interface

When CLI is used, we identify the mode by the command-line prompts unique message prompt that belongs to that mode.
- **Switch(config-line)#**
- **Switch(config-if)#**

By entering different modes, users get different privileges according to the level of the mode that is entered.

### Navigation Between Modes in IOS

Various commands prompts for navigation:
- enable - move to EXEC to privileged EXEC mode
- disable - return from privilege to regular EXEC mode
- configure terminal - used in privileged EXEC mode to move in and out of global configuration mode
- line - enter line and a number for the requested subconfig mode
	- line console 0
- exit - duuh
- end - moves from subconfig mode to the privileged EXEC mode
	- or CTRL-Z
- interface FastEthernet 0/1 - interface moves from one subconfig to another. 
- commands that are used in regular global config mode, can also be used in sub-config mode.
---

## The Command Structure
> Topic that covers the basic structure of commands for the Cisco IOS.

### Basic IOS Command Structure
A network admin needs to know the basic and fundamental IOS command structure to be able to use the CLI for device configuration. 

The Cisco IOS devices supports many commands, and each of them has a specific format or syntax, that can only be executed when in the correct mode. Below we see the general syntax for a command. We observe that the command is followed by any appropriate keywords and arguments.

![[Screenshot 2023-08-31 at 16.25.15.png]]

- **Keyword** - this is a specific parameter defined in the operating system.
- **Argument** - not predefined; a value or variable defined by the user

A command might require one or more arguments. To determine the keywords and arguments required for a command, refer to the command syntax. The syntax provides the pattern, or format, that must be used when entering a command.

| Convention   | Description                                                                      |
| ------------ | -------------------------------------------------------------------------------- |
| **boldface** | Boldface text indicates commands and keywords that you enter literally as shown. |
| *Italics*    | Italic text indicates arguments for which you supply values.                     |
| [X]          | Square brackets indicate an optional element (keyword or argument).              |
| {x}          | Braces indicate a required element (keyword or argument).                        |
| [x {y / z }]             |         Braces and vertical lines within square brackets indicate a required choice within an optional element. Spaces are used to clearly delineate parts of the command.                                                                         |


### Hot Keys & Shortcuts
The IOS CLI provides hot keys and shortcuts that make configuring, monitoring, and troubleshooting easier.

Commands and keywords can be shortened to the minimum number of characters that identify a unique selection. For example, the **configure** command can be shortened to **conf** because **configure** is the only command that begins with **conf**. An even shorter version, **con**, will not work because more than one command begins with **con**. Keywords can also be shortened.

The table lists keystrokes to enhance command line editing.

| Keystroke                  | Description |
| -------------------------- | ----------- |
| Tab                        |   Completes a partial command name entry.          |
| Backspace                  |    Erases the character to the left of the cursor.         |
| Ctrl+D                     |    Erases the character at the cursor.         |
| Ctrl+K                     |     Erases all characters from the cursor to the end of the command line.        |
| Esc D                      |    Erases all characters from the cursor to the end of the word.         |
| Crl+U or Ctrl+X            |     Erases all characters from the cursor back to the beginning of the command line.        |
| Ctrl+W                     |       Erases the word to the left of the cursor.      |
| Ctrl+A                     |Moves the cursor to the beginning of the line.             |
| Left Arrow or Ctrl+B       |   Moves the cursor one character to the left.          |
| Esc B                      | Moves the cursor back one word to the left.            |
| Esc F                      |             |
| Right Arrow or Ctrl+P      |             |
| Down Arrow or Ctrl+N       |             |
| Ctrl+R or Ctrl+I or Ctrl+L |             |
|                            |             |

**Note**: While the **Delete** key typically deletes the character to the right of the prompt, the IOS command structure does not recognize the Delete key.

When a command output produces more text than can be displayed in a terminal window, the IOS will display a **“--More--”** prompt. The following table describes the keystrokes that can be used when this prompt is displayed.

---
## Basic Device Configuration

### Naming and Device Names
> The first configuration command on any device should be to give it a unique device name or hostname. By default, all devices are assigned a factory default name. For example, a Cisco IOS switch is "Switch."

The problem is if all switches in a network were left with their default names, it would be difficult to identify a specific device. For instance, how would you know that you are connected to the right device when accessing it remotely using SSH? The hostname provides confirmation that you are connected to the correct device.

The default name should be changed to something more descriptive. By choosing names wisely, it is easier to remember, document, and identify network devices. Here are some important naming guidelines for hosts:

- Start with a letter
- Contain no spaces
- End with a letter or digit
- Use only letters, digits, and dashes
- Be less than 64 characters in length

When the naming convention has been identified, the next step is to use the CLI to apply the names to the devices. As shown in the example, from the privileged EXEC mode, access the global configuration mode by entering the **configure terminal** command. Notice the change in the command prompt.
![[Pasted image 20230831164330.png]]
From global configuration mode, enter the command **hostname** followed by the name of the switch and press **Enter**. Notice the change in the command prompt name.

**Note**: To return the switch to the default prompt, use the **no hostname** global config command.

Always make sure the documentation is updated each time a device is added or modified. Identify devices in the documentation by their location, purpose, and address.

### Password guidelines
The use of weak or easily guessed passwords continues to be the biggest security concern of organizations. Network devices, including home wireless routers, should always have passwords configured to limit administrative access.

Cisco IOS can be configured to use hierarchical mode passwords to allow different access privileges to a network device.

All networking devices should limit administrative access by securing privileged EXEC, user EXEC, and remote Telnet access with passwords. In addition, all passwords should be encrypted and legal notifications provided.

When choosing passwords, use strong passwords that are not easily guessed. There are some key points to consider when choosing passwords:

- Use passwords that are more than eight characters in length.
- Use a combination of upper and lowercase letters, numbers, special characters, and/or numeric sequences.
- Avoid using the same password for all devices.
- Do not use common words because they are easily guessed.

Use an internet search to find a password generator. Many will allow you to set the length, character set, and other parameters.

### Configure Passwords
When you initially connect to a device, you are in user EXEC mode. This mode is secured using the console.

To secure user EXEC mode access, enter line console configuration mode using the **line console 0** global configuration command, as shown in the example. The zero is used to represent the first (and in most cases the only) console interface. Next, specify the user EXEC mode password using the **password** _password_ command. Finally, enable user EXEC access using the **login** command.
![[Pasted image 20230831164658.png]]

Console access will now require a password before allowing access to the user EXEC mode.

To have administrator access to all IOS commands including configuring a device, you must gain privileged EXEC mode access. It is the most important access method because it provides complete access to the device.

To secure privileged EXEC access, use the **enable secret** _password_ global config command, as shown in the example.
![[Pasted image 20230831164800.png]]
Virtual terminal (VTY) lines enable remote access using Telnet or SSH to the device. Many Cisco switches support up to 16 VTY lines that are numbered 0 to 15.

To secure VTY lines, enter line VTY mode using the **line vty 0 15** global config command. Next, specify the VTY password using the **password** _password_ command. Lastly, enable VTY access using the **login** command.

An example of securing the VTY lines on a switch is shown.
![[Pasted image 20230831164918.png]]

### Encrypt Password
The startup-config and running-config files display most passwords in plaintext. This is a security threat because anyone can discover the passwords if they have access to these files.

To encrypt all plaintext passwords, use the **service password-encryption** global config command as shown in the example.
![[Pasted image 20230831165110.png]]

The command applies weak encryption to all unencrypted passwords. This encryption applies only to passwords in the configuration file, not to passwords as they are sent over the network. The purpose of this command is to keep unauthorized individuals from viewing passwords in the configuration file.

Use the **show running-config** command to verify that passwords are now encrypted.

![[Pasted image 20230831165148.png]]

### Banner Messages
Although requiring passwords is one way to keep unauthorized personnel out of a network, it is vital to provide a method for declaring that only authorized personnel should attempt to access the device. To do this, add a banner to the device output. Banners can be an important part of the legal process in the event that someone is prosecuted for breaking into a device. Some legal systems do not allow prosecution, or even the monitoring of users, unless a notification is visible.

To create a banner message of the day on a network device, use the **banner motd #** _the message of the day_ **#** global config command. The “#” in the command syntax is called the delimiting character. It is entered before and after the message. The delimiting character can be any character as long as it does not occur in the message. For this reason, symbols such as the "#" are often used. After the command is executed, the banner will be displayed on all subsequent attempts to access the device until the banner is removed.

The following example shows the steps to configure the banner on Sw-Floor-1.
![[Pasted image 20230831165506.png]]
---

## Save Configurations
> This topic will show you how to save your configurations

### Configuration Files
There are two system files that store the device configuration:
- **startup-config**: This is the configuration file that is saved and stored in NVRAM.
	- It contains all the commands that will be used by the device upon startup or reboot. 
	- Flash does not lose its contents when the device is powered off
- **running-config**: stored in Random Access Memory (RAM). 
	- It reflects current configuration. 
	- Modifying a running configuration affects the operation of a Cisco device immediately. 
	- RAM is volatile memory, meaning it loses all of its content when the device is powered off or restarted.

The **show running-config** privileged EXEC mode command is used to view the running config. As shown in the example, the command will list the complete configuration currently stored in RAM.
![[Pasted image 20230831175910.png]]
To view the startup configuration file, use the **show startup-config** privileged EXEC command.

If power to the device is lost, or if the device is restarted, all configuration changes will be lost unless they have been saved. To save changes made to the running configuration to the startup configuration file, use the **copy running-config startup-config** privileged EXEC mode command.

### Alter the Running Configuration
If changes made to the running config do not have the desired effect and the running-config has not yet been saved, you can restore the device to its previous configuration. Remove the changed commands individually, or reload the device using the **reload** privileged EXEC mode command to restore the startup-config.
- **reload**
- The downside to using the **reload** command to remove an unsaved running config is the brief amount of time the device will be offline, causing network downtime.
- When a reload is initiated, the IOS will detect that the running config has changes that were not saved to the startup configuration. A prompt will appear to ask whether to save the changes. To discard the changes, enter **n** or **no**.

Alternatively, if undesired changes were saved to the startup config, it may be necessary to clear all the configurations. This requires erasing the startup config and restarting the device. The startup config is removed by using the **erase startup-config** privileged EXEC mode command. After the command is issued, the switch will prompt you for confirmation. Press **Enter** to accept.

After removing the startup config from NVRAM, reload the device to remove the current running config file from RAM. On reload, a switch will load the default startup config that originally shipped with the device.

### Capture Configuration to a Text File
We can easily save configuration files and archive them to a text document. By doing these sequence of steps, it ensures that a working copy of the configuration file is available for editing or reuse later. 

For example, assume that a switch has been configured, and the running config has been saved on the device.

**Step 1.** Open terminal emulation software, such as PuTTY or Tera Term, that is already connected to a switch.
![[Pasted image 20230831181053.png]]
**Step 2.** Enable logging in the terminal software and assign a name and file location to save the log file. The figure displays that **All session output** will be captured to the file specified (i.e., MySwitchLogs).
![[Pasted image 20230831181114.png]]
**Step 3.** Execute the **show running-config** or **show startup-config** command at the privileged EXEC prompt. Text displayed in the terminal window will be placed into the chosen file.
![[Pasted image 20230831181133.png]]
**Step 4.** Disable logging in the terminal software. The figure shows how to disable logging by choosing the **None** session logging option.
![[Pasted image 20230831181153.png]]
The text file created can be used as a record of how the device is currently implemented. The file could require editing before being used to restore a saved configuration to a device.

To restore a configuration file to a device:
**Step 1.** Enter global configuration mode on the device.
**Step 2.** Copy and paste the text file into the terminal window connected to the switch.

The text in the file will be applied as commands in the CLI and become the running configuration on the device. This is a convenient method of manually configuring a device.

---
## Ports and Addresses
> For the end devices to communicate with each other, we must ensure that each of them has an appropriate IP address and its correctly connected. We will take a deeper look at is in this section.

### IP Addresses
The use of [[Network Layer#The Internet Protocol|IP]] addresses is the primary means of enabling devices to locate one another and establish end-to-end communication on the internet. Each end device on a network must be configured with an IP address. Examples of end devices include these:
- Computers (work stations, laptops, file servers, web servers)
- Network printers
- VoIP phones
- Security cameras
- Smart phones
- Mobile handheld devices (such as wireless barcode scanners)

The structure of an [[Network Layer#IPv4|IPv4]] address is called dotted decimal notation and is represented by four decimal numbers between 0 and 255. IPv4 addresses are assigned to individual devices connected to a network.

With the [[Network Layer#IPv4|IPv4]] address, a subnet mask is also necessary. An IPv4 subnet mask is a 32-bit value that differentiates the network portion of the address from the host portion. Coupled with the IPv4 address, the subnet mask determines to which subnet the device is a member.

[[Network Layer#IPv6|IPv6]] addresses are 128 bits in length and written as a string of hexadecimal values. Every four bits is represented by a single hexadecimal digit; for a total of 32 hexadecimal values. Groups of four hexadecimal digits are separated by a colon (:) . IPv6 addresses are not case-sensitive and can be written in either lowercase or uppercase.

### Interfaces and Ports
Network communications depends on end user device interfaces, network device interfaces, and the cables that is connecting them. 
Each physical interface has specifications, or standards, that define it.  A cable connecting to the interface must be designed so that it matches the physical standard of the interface. 
Types of network media:
- twisted-pair copper cables
- fiber-optic cables
- coaxial cables
- wireless
![[Pasted image 20230831190419.png]]

Every network media type has its own features and benefits. Not all of them have the same characteristics, and not all media are appropriate for the same purpose. Some of the differences between the various types of media are:
- Distance the media can successfully carry a signal
- Environment in which the media is to be installed
- Amount of data and the speed at which it must be transmitted
- Cost of the media and installation

Not only does each link on the internet require a specific network media type, but each link also requires a particular network technology. For example, Ethernet is the most common local-area network (LAN) technology used today. Ethernet ports are found on end-user devices, switch devices, and other networking devices that can physically connect to the network using a cable.

Cisco IOS Layer 2 switches have physical ports for devices to connect. These ports do not support Layer 3 IP addresses. Therefore, switches have one or more switch virtual interfaces (SVIs). These are virtual interfaces because there is no physical hardware on the device associated with it. An SVI is created in software.

The virtual interface lets you remotely manage a switch over a network using IPv4 and IPv6. Each switch comes with one SVI appearing in the default configuration "out-of-the-box." The default SVI is interface VLAN1.
**Note**: A Layer 2 switch does not need an IP address. The IP address assigned to the SVI is used to remotely access the switch. An IP address is not necessary for the switch to perform its operations.

---
## Configure IP Addressing
> End devices in your network need an IP address to communicate with other devices. Therefore we have to implement basic connectivity by configuring IP addressing on switches and PCs.

### Manual IP Address Configuration for End Devices
IPv4 address information can be entered into end devices manually, or as usual by the [[Network Layer#DHCP|DHCP]] protocol(Dynamic Host Configuration Protocol).

To manually configure an IPv4 address on a Windows host, open the **Control Panel -> Network Sharing Center -> Change adapter settings** and choose the adapter. Next right-click and select **Properties** to display the **Local Area Connection Properties**, as shown in the figure.
![[Pasted image 20230831191258.png]]

Highlight Internet Protocol Version 4 (TCP/IPv4) and click **Properties** to open the **Internet Protocol Version 4 ([[TCP|TCP]]/IPv4) Properties** window, shown in the figure. Configure the IPv4 address and subnet mask information, and default gateway.
**Note**: IPv6 addressing and configuration options are similar to IPv4.
![[Pasted image 20230831191336.png]]
**Note**: The [[Application Layer#DNS|DNS ]]server addresses are the IPv4 and IPv6 addresses of the Domain Name System (DNS) servers, which are used to translate IP addresses to domain names, such as

### Automatic IP Address Configuration for End Devices
End devices typically default to using [[Network Layer#DHCP|DHCP]] for automatic [[Network Layer#IPv4|IPv4 ]]address configuration. [[Network Layer#DHCP|DHCP]] is a technology that is used in almost every network. The best way to understand why [[Network Layer#DHCP|DHCP]] is so popular is by considering all the extra work that would have to take place without it.

In a network, DHCP enables automatic IPv4 address configuration for every end device that is DHCP-enabled. Imagine the amount of time it would take if every time you connected to the network, you had to manually enter the IPv4 address, the subnet mask, the default gateway, and the DNS server. Multiply that by every user and every device in an organisation and you see the problem. Manual configuration also increases the chance of misconfiguration by duplicating another device’s IPv4 address.

As shown in the figure, to configure DHCP on a Windows PC, you only need to select **Obtain an IP address automatically** and **Obtain DNS server address automatically**. Your PC will search out a DHCP server and be assigned the address settings necessary to communicate on the network.

**Note**: IPv6 uses DHCPv6 and SLAAC (Stateless Address Autoconfiguration) for dynamic address allocation.
![[Pasted image 20230831192659.png]]

- Ipconfig

### Switch Virtual Interface Config
To access the switch remotely, an IP address and a subnet mask must be configured on the SVI. To configure an SVI on a switch, use the **interface vlan 1** global configuration command. Vlan 1 is not an actual physical interface but a virtual one. Next assign an IPv4 address using the **ip address** _ip-address subnet-mask_ interface configuration command. Finally, enable the virtual interface using the **no shutdown** interface configuration command.

After these commands are configured, the switch has all the IPv4 elements ready for communication over the network.

**Note**: Similar to a Windows hosts, switches configured with an IPv4 address will typically also need to have a default gateway assigned. This can be done using the **ip default-gateway** _ip-address_ global configuration command. The _ip-address_ parameter would be the IPv4 address of the local router on the network, as shown in the example. However, in this module you will only be configuring a network with switches and hosts. Routers will be introduced later.
![[Screenshot 2023-08-31 at 19.28.26.png]]


## Verify Connectivity






