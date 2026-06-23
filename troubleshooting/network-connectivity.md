# Network Connectivity Troubleshooting

## Issue

Ubuntu VM was unable to communicate with the Windows VM over the Host-Only network.

## Environment

- Windows VM: WIN-ITLAB
- Ubuntu VM: UBUNTU-ITLAB
- Network Type: VirtualBox Host-Only Network
- Subnet: 192.168.56.0/24

## Impact

Communication between Windows and Ubuntu virtual machines was not possible, preventing further networking exercises and service testing.

## Symptoms

### Successful

* Windows VM could ping Ubuntu VM.
* Static IP addresses were configured correctly.

### Failed

* Ubuntu VM could not ping Windows VM.
* ICMP requests resulted in 100% packet loss.

## Investigation

### Step 1 - Verify IP Configuration

Confirmed both systems were configured on the same subnet.

#### Windows

```text
IP Address: 192.168.56.10
Subnet Mask: 255.255.255.0
```

#### Ubuntu

```text
IP Address: 192.168.56.20
Subnet Mask: 255.255.255.0
```

### Step 2 - Verify Host-Only Network

Confirmed both virtual machines were connected to:

```text
VirtualBox Host-Only Ethernet Adapter #2
```

### Step 3 - Verify Firewall Configuration

Temporarily disabled Windows Defender Firewall for Private Networks.

Result:

```text
Issue persisted.
```

### Step 4 - Enable ICMP Echo Requests

Enabled:

```text
Windows Defender Firewall
→ Advanced Security
→ Inbound Rules
→ File and Printer Sharing (Echo Request - ICMPv4-In)
```

Result:

```text
Issue persisted.
```

### Step 5 - Investigate Network Profile

Discovered the Host-Only adapter was classified as:

```text
Public Network
```

instead of:

```text
Private Network
```

### Step 6 - Modify Network Category

Executed PowerShell as Administrator:

```powershell
Get-NetConnectionProfile
Set-NetConnectionProfile -InterfaceIndex X -NetworkCategory Private
```
X = Actual InterfaceIndex Number

## Root Cause

The Windows Host-Only network adapter was automatically assigned a Public Network profile. This caused Windows to restrict inbound ICMP traffic, preventing Ubuntu from successfully pinging the Windows VM.

## Resolution

Changed the Host-Only adapter network profile from Public to Private.

## Verification

The following tests were performed:

- Windows → Ubuntu ICMP successful
- Ubuntu → Windows ICMP successful
- Both systems reachable on the same subnet

Result: Issue resolved successfully.

## Result

Successful bidirectional communication:

```text
Windows → Ubuntu   SUCCESS
Ubuntu → Windows   SUCCESS

WIN-ITLAB <---> UBUNTU-ITLAB   SUCCESS
```

## Lessons Learned

* Verify network profiles when troubleshooting Windows connectivity issues.
* Confirm firewall and ICMP rules before investigating routing problems.
* Validate IP addressing and subnet configuration early in the troubleshooting process.
* Use a structured troubleshooting methodology: Verify → Isolate → Test → Resolve.

## Commands Used

### Windows

```powershell
Get-NetConnectionProfile
Set-NetConnectionProfile -InterfaceIndex X -NetworkCategory Private
ping 192.168.56.20
```

### Ubuntu

```bash
ip addr
ping 192.168.56.10
```