# The Summrize of the below steps 1 -> 9:
## Secure management access to a switch.

### - Assign a device name.
### - Secure user EXEC mode access.
### - Secure privileged EXEC mode access.
### - Secure VTY access.
### - Encrypt all plaintext passwords.
### - Display a login banner.
### - copy running-config startup-config = copy run start
1.  As a security feature, the Cisco IOS software separates management access into 
    the following two command modes:

    - User EXEC Mode - This mode has limited capabilities but is useful for basic operations. It allows only a limited number of basic monitoring commands but does not allow the execution of any commands that might change the configuration of the device. The user EXEC mode is identified by the CLI prompt that ends with the > symbol.

    - Privileged EXEC Mode - To execute configuration commands, a network administrator must access privileged EXEC mode. Higher configuration modes, like global configuration mode, can only be reached from privileged EXEC mode. The privileged EXEC mode can be identified by the prompt ending with the # symbol.


2.  Navigate Between IOS Modes, Command are
    `Switch(config)# line console 0`
    `Switch(config-line)# exit`
    `Switch(config)#`

3.  To move from any subconfiguration mode of the global configuration mode to the mode one step above it in the hierarchy of modes, enter the exit command.
    `Switch(config-line)# end` 
    `Switch#`

4.  You can also move directly from one subconfiguration mode to another. Notice how after selecting an interface, the command prompt changes from (config-line)# to (config-if)#.
    `Switch(config-line)# interface FastEthernet 0/1`
    `Switch(config-if)#`

5.  Device Names:
    - Start with a letter
    - Contain no spaces
    - End with a letter or digit
    - Use only letters, digits, and dashes
    - Be less than 64 characters in length
    `Switch# configure terminal`
    `Switch(config)# hostname Sw-Floor-1`
    `Sw-Floor-1(config)#`
    * Note: To return the switch to the default prompt, use the no hostname global config command.

6. Configure Passwords: When you initially connect to a device, you are in user EXEC mode. This mode is secured using the console.
To secure user EXEC mode access, enter line console configuration mode using the line console 0 global configuration command, as shown in the example. The zero is used to represent the first (and in most cases the only) console interface. Next, specify the user EXEC mode password using the password password command. Finally, enable user EXEC access using the login command.
        `Sw-Floor-1# configure terminal`
        `Sw-Floor-1(config)# line console 0`
        `Sw-Floor-1(config-line)# password cisco`
        `Sw-Floor-1(config-line)# login`
        `Sw-Floor-1(config-line)# end`
        `Sw-Floor-1#`
        
   - Console access will now require a password before allowing access to the user EXEC mode.
   - To secure privileged EXEC access, use the enable secret password global config command, as shown in the example.

        `Sw-Floor-1# configure terminal`
        `Sw-Floor-1(config)# enable secret class`
        `Sw-Floor-1(config)# exit`
        `Sw-Floor-1#`


7.  Virtual terminal (VTY) lines enable remote access using Telnet or SSH to the device. Many Cisco switches support up to 16 VTY lines that are numbered 0 to 15. To secure VTY lines, enter line VTY mode using the line vty 0 15 global config command. Next, specify the VTY password using the password password command. Lastly, enable VTY access using the login command.An example of securing the VTY lines on a switch is shown.

    `Sw-Floor-1# configure terminal`
    `Sw-Floor-1(config)# line vty 0 15`
    `Sw-Floor-1(config-line)# password cisco `
    `Sw-Floor-1(config-line)# login `
    `Sw-Floor-1(config-line)# end`
    `Sw-Floor-1#`

8.  Encrypt Passwords: The startup-config and running-config files display most passwords in plaintext. This is a security threat because anyone can discover the passwords if they have access to these files.
To encrypt all plaintext passwords, use the service password-encryption global config command as shown in the example.
    `Sw-Floor-1# configure terminal`
    `Sw-Floor-1(config)# service password-encryption`
    `Sw-Floor-1(config)#`
    - Use the show running-config command to verify that passwords are now encrypted.
        `Sw-Floor-1(config)# end`
        `Sw-Floor-1# show running-config`

9.  Banner Messages: To create a banner message of the day on a network device, use the banner motd # the message of the day # global config command. The “#” in the command syntax is called the delimiting character. It is entered before and after the message. The delimiting character can be any character as long as it does not occur in the message. For this reason, symbols such as the "#" are often used. After the command is executed, the banner will be displayed on all subsequent attempts to access the device until the banner is removed.

    `Sw-Floor-1# configure terminal`
    `Sw-Floor-1(config)# banner motd #Authorized Access Only#`

10. Configuration Files: There are two system files that store the device configuration:

    -   startup-config - This is the saved configuration file that is stored in NVRAM. It contains all the commands that will be used by the device upon startup or reboot. Flash does not lose its contents when the device is powered off.
        + The `show running-config` privileged EXEC mode command is used to view the running config. As shown in the example, the command will list the complete configuration currently stored in RAM.

    -   running-config - This is stored in Random Access Memory (RAM). It reflects the current configuration. Modifying a running configuration affects the operation of a Cisco device immediately. RAM is volatile memory. It loses all of its content when the device is powered off or restarted.
        + To view the startup configuration file, use the `show startup-config` privileged EXEC command.
          
    - If power to the device is lost, or if the device is restarted, all configuration changes will be lost unless they have been saved. To save changes made to the running configuration to the startup configuration file, use the copy running-config startup-config privileged EXEC mode command.

11. Alter the Running Configuration: If changes made to the running config do not have the desired effect and the running-config has not yet been saved, you can restore the device to its previous configuration. Remove the changed commands individually, or reload the device using the `reload` privileged EXEC mode command to restore the startup-config.
    - The downside to using the reload command to remove an unsaved running config is the brief amount of time the device will be offline, causing network downtime.

12. Alternatively, if undesired changes were saved to the startup config, it may be necessary to clear all the configurations. This requires erasing the startup config and restarting the device. The startup config is removed by using the `erase startup-config` privileged EXEC mode command. After the command is issued, the switch will prompt you for confirmation. Press `Enter` to accept.
    - After removing the startup config from NVRAM, reload the device to remove the current running config file from RAM. On reload, a switch will load the default startup config that originally shipped with the device.
    - We also can reverse the load of configuration: `copy startup-config running-config` in this moment the configurations will be merged. 2.5.3 section. `copy running-config startup-config = copy run start`

### Ports and Addresses

13. IP Addresses: 

    - IPv6 addresses are 128 bits in length and written as a string of hexadecimal values. Every four bits is represented by a single hexadecimal digit; for a total of 32 hexadecimal values. Groups of four hexadecimal digits are separated by a colon (:) . IPv6 addresses are not case-sensitive and can be written in either lowercase or uppercase.

    - The structure of an IPv4 address is called dotted decimal notation and is represented by four decimal numbers between 0 and 255. IPv4 addresses are assigned to individual devices connected to a network.

Note: IP in this course refers to both the IPv4 and IPv6 protocols. IPv6 is the most recent version of IP and is replacing the more common IPv4.

With the IPv4 address, a subnet mask is also necessary. An IPv4 subnet mask is a 32-bit value that differentiates the network portion of the address from the host portion. Coupled with the IPv4 address, the subnet mask determines to which subnet the device is a member.

The example in the figure displays the IPv4 address (192.168.1.10), subnet mask (255.255.255.0), and default gateway (192.168.1.1) assigned to a host. The default gateway address is the IP address of the router that the host will use to access remote networks, including the internet.

- Not only does each link on the internet require a specific network media type, but each link also requires a particular network technology. For example, Ethernet is the most common local-area network (LAN) technology used today. Ethernet ports are found on end-user devices, switch devices, and other networking devices that can physically connect to the network using a cable.

Cisco IOS Layer 2 switches have physical ports for devices to connect. These ports do not support Layer 3 IP addresses. Therefore, switches have one or more switch virtual interfaces (SVIs). These are virtual interfaces because there is no physical hardware on the device associated with it. An SVI is created in software.

The virtual interface lets you remotely manage a switch over a network using IPv4 and IPv6. Each switch comes with one SVI appearing in the default configuration "out-of-the-box." The default SVI is interface VLAN1.

Note: A Layer 2 switch does not need an IP address. The IP address assigned to the SVI is used to remotely access the switch. An IP address is not necessary for the switch to perform its operations.

### Configure IP Addressing

13. Manual IP Address Configuration for End Devices:

    - IPv4 address information can be entered into end devices manually, or automatically using Dynamic Host Configuration Protocol (DHCP).
    - Note: The DNS server addresses are the IPv4 and IPv6 addresses of the Domain Name System (DNS) servers, which are used to translate IP addresses to domain names, such as www.cisco.com.

14. Automatic IP Address Configuration for End Devices
    - End devices typically default to using DHCP for automatic IPv4 address configuration. DHCP is a technology that is used in almost every network. The best way to understand why DHCP is so popular is by considering all the extra work that would have to take place without it.
    - Note: IPv6 uses DHCPv6 and SLAAC (Stateless Address Autoconfiguration) for dynamic address allocation.

15. Syntax Checker - Verify Windows PC IP Configuration:
    `C:\>ipconfig`

16. Switch Virtual Interface Configuration:
    - To access the switch remotely, an IP address and a subnet mask must be configured on the SVI. To configure an SVI on a switch, use the interface vlan 1 global configuration command. Vlan 1 is not an actual physical interface but a virtual one. Next assign an IPv4 address using the ip address ip-address subnet-mask interface configuration command. Finally, enable the virtual interface using the no shutdown interface configuration command.

    - After these commands are configured, the switch has all the IPv4 elements ready for communication over the network.

    - Note: Similar to a Windows hosts, switches configured with an IPv4 address will typically also need to have a default gateway assigned. This can be done using the ip default-gateway ip-address global configuration command. The ip-address parameter would be the IPv4 address of the local router on the network, as shown in the example. However, in this module you will only be configuring a network with switches and hosts. Routers will be introduced later.

    `Sw-Floor-1# configure terminal`
    `Sw-Floor-1(config)# interface vlan 1`
    `Sw-Floor-1(config-if)# ip address 192.168.1.20 255.255.255.0`
    `Sw-Floor-1(config-if)# no shutdown`
    `Sw-Floor-1(config-if)# exit`
    `Sw-Floor-1(config)# ip default-gateway 192.168.1.1`

17. Verify Connectivity:
    * In the same way that you use commands and utilities like ipconfig to verify the network configuration of a PC host, you also use commands to verify the interfaces and address settings of intermediary devices like switches and routers.

    * Click Play in the figure to view a video demonstration of the show ip interface brief command. This command is useful for verifying the condition of the switch interfaces.

18. Tricky question:
    - To what subnet does the IP address 10.1.100.50 belong if a subnet mask of 255.255.0.0 is used?
        * 10.1.0.0
        * Topic 2.6.0 - The purpose of a subnet mask is to separate the network portion of the address from the host portion of the IP address. The network portion of the IP address is identified by all binary 1s in the subnet mask. Using a subnet mask of 255.255.0.0 identifies the first two octets of the IP address as the network portion.