# Day 1 - Building the Lab & Networking

## Objective

Build a virtualized Windows and Ubuntu environment using VirtualBox and establish network connectivity between both systems.

---

## Environment

### Host Machine

* Operating System: Windows 10
* RAM: 32 GB (29.9 GB usable)
* Free Disk Space:

  * C: Drive - 119 GB
  * F: Drive - 165 GB
* Virtualization: Enabled

---

## Software and Resources

### Virtualization Platform

* Oracle VirtualBox

### Operating System Images

* Windows 10
* Ubuntu 26.04 LTS

---

## Virtual Machines Created

### WIN-ITLAB

| Setting         | Value               |
| --------------- | ------------------- |
| OS              | Windows 10 (64-bit) |
| RAM             | 4096 MB             |
| CPU             | 2 vCPUs             |
| Disk            | 50 GB (Dynamic VDI) |
| Username        | adminuser           |
| Hostname        | WIN-ITLAB           |

### UBUNTU-ITLAB

| Setting  | Value               |
| -------- | ------------------- |
| OS       | Ubuntu 26.04 LTS    |
| RAM      | 4096 MB             |
| CPU      | 2 vCPUs             |
| Disk     | 25 GB (Dynamic VDI) |
| Username | employee1           |
| Hostname | UBUNTU-ITLAB        |

---

## Project Structure

```text
IT-HomeLab/
│
├── screenshots/
├── docs/
├── troubleshooting/
└── README.md
```

---

## Network Configuration

### Host-Only Network

Created a VirtualBox Host-Only Network with the following configuration:

| Setting      | Value                                    |
| ------------ | ---------------------------------------- |
| Adapter      | VirtualBox Host-Only Ethernet Adapter #2 |
| Network      | 192.168.56.0/24                          |
| Host Address | 192.168.56.1                             |
| Subnet Mask  | 255.255.255.0                            |

### Static IP Assignment

#### Windows VM

| Setting     | Value         |
| ----------- | ------------- |
| IP Address  | 192.168.56.10 |
| Subnet Mask | 255.255.255.0 |
| DNS Server  | 8.8.8.8       |

#### Ubuntu VM

| Setting     | Value         |
| ----------- | ------------- |
| IP Address  | 192.168.56.20 |
| Subnet Mask | 255.255.255.0 |

#### Network Diagram

```text
Host Machine (Windows 10)
│
├── WIN-ITLAB
│   └── 192.168.56.10
│
└── UBUNTU-ITLAB
    └── 192.168.56.20
```

Host-Only Network
192.168.56.0/24

---

## Validation

### Connectivity Testing

Successfully verified communication between both virtual machines:

* Windows → Ubuntu: Successful
* Ubuntu → Windows: Successful

---

## Skills Practiced

* Virtualization
* Virtual Machine Deployment
* Linux Administration
* Windows Administration
* Static IP Configuration
* TCP/IP Networking
* Host-Only Networking
* Network Troubleshooting
* Windows Firewall Configuration

---

## Evidence

Screenshots collected:

* windows-ipconfig.png
![windows-ipconfig.png](./screenshots/windows-ipconfig.png)

* ubuntu-ipaddr.png
![ubuntu-ipaddr.png](./screenshots/ubuntu-ipaddr.png)

* ping-ubuntu.png
![ping-ubuntu.png](./screenshots/ping-ubuntu.png)

* ping-windows.png
![ping-windows.png](./screenshots/ping-windows.png)

---

## Outcome

Successfully built a Windows and Ubuntu virtual lab environment and established bidirectional communication between both systems using Host-Only networking.

---

## Key Commands Used

### Windows
```
ipconfig  
ping 192.168.56.20  
Get-NetConnectionProfile  
Set-NetConnectionProfile -InterfaceIndex X -NetworkCategory Private
```
### Ubuntu
```
ip addr  
ls /etc/netplan/  
sudo nano /etc/netplan/01-network-manager-all.yaml  
sudo netplan apply  
ping 192.168.56.10
```
