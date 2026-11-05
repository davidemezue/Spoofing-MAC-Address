# Spoofing Your MAC Address

## Lab Objective

Learn how to use macchanger to spoof your MAC address.

## Lab Purpose

Macchanger is a tool which allows us to change our network card’s hardware MAC address to a random address. This is useful when performing penetration tests or other audits in order to evade detection.

## Lab Tool

- Kali Linux

## Lab Topology

You can use Kali Linux in a VM for this lab.

## Lab Walkthrough

### Task 1: Viewing Macchanger Help and Current MAC Address

I will be using Kali Linux (root) for this lab as macchanger comes pre-installed on Kali.

We will begin by viewing the help screen for this tool by typing the following:

```bash
macchanger -h
```

We will first check what our current MAC address is using the following command:

```bash
macchanger -s eth0
```

### Task 2: Changing the MAC Address to a Random Address

We must first turn off the interface we are going to change the MAC address for, otherwise the tool will not work.

To do this, use these following commands:

```bash
ifconfig eth0 down
ifconfig
```

We can now set a random MAC address for this interface by executing the following:

```bash
macchanger -r eth0
```

We can now bring our interface back up using this command:

```bash
ifconfig eth0 up
```

Finally, we can view our MAC address for this interface again to confirm that it has been changed, using this command:

```bash
macchanger -s eth 0
```

### Task 3: Changing the MAC Address to a Specific Address

We can also change our MAC address to a specific address if we want to masquerade as a specific device.

There are actually 4 sets of Locally Administered Address Ranges that can be used on your network without fear of conflict, assuming no one else has assigned these on your network:

```text
x2-xx-xx-xx-xx-xx
x6-xx-xx-xx-xx-xx
xA-xx-xx-xx-xx-xx
xE-xx-xx-xx-xx-xx
```

We can do this using the following commands:

```bash
ifconfig eth0 down
macchanger -m d4:b1:10:d8:57:73 eth0
```

```bash
ifconfig eth0 up
ifconfig
```

```bash
macchanger -s eth0
```

### Task 4: Finding Hardware Vendor MAC Address Prefixes

We can use the "-l" option to find the MAC address prefix of specific hardware vendors, allowing us to masquerade as a device from one of these vendors:

```bash
macchanger -l
```

### Task 5: Reverting to the Original Permanent MAC Address

To revert to our original permanent MAC address, we can use the following set of commands:

```bash
ifconfig eth0 down
macchanger -p eth0
```

```bash
ifconfig eth0 up
```
