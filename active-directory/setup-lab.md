# Active Directory Home Lab Setup for SOC Monitoring

*This project documents the deployment of a scalable Active Directory environment designed for security monitoring, attack simulation, and log analysis.*

## Network Architecture

- **Network Type:** Internal Network (`intnet`) 
- **Subnet:** `192.168.1.0/24` 
- **Domain Controller (DC) IP:** `192.168.1.1` 
- **Windows 10 Workstation (WS1) IP:** `192.168.1.10`

## Domain Controller Deployment

*A new forest was established on Windows Server, with **AD DS** (Active Directory Domain Services) and **DNS** roles fully promoted.*

- **Domain Name:** `lewa9-soc.lab` 
- **NetBIOS Name:** `LEWA9-SOC`

### Step - 1. Network Configuration

First of all to imitate corporate network system in our virtual machine we need set-up network connection, also its helpfull for close lab experiments. It also isolates environment from host machine to prevent accidental interference.

It need to be done in Network settings for both machines.

![[Pasted image 20260426201126.png]]

### Step - 2. Setting Server IP address

To build private network system, for server work it need static IP. So there assign `192.168.1.1` to the Domain Controller. The server points to itself `192.168.1.1`  for DNS resolution to manage the domain locally.

![[Pasted image 20260426201106.png]]

### Step - 3. AD DS & DNS Role Installation

Giving server AD DS and DNS roles and features, after that in server manager we can confirm roles assigned correctly in left bar.

![[Pasted image 20260426205208.png]]

### Step - 4. Forest Creation

Finalizing the domain setup, and giving root domain name. For futher proper lab work.

![[Pasted image 20260426205945.png]]

### Step - 5. Active Directory Inventory (OUs & Users)

For future tests, creating the `HQ` and `Lab-Users` OUs and the `lewa_rob` account.

![[Pasted image 20260426212013.png]]

### Step - 6. Advanced Audit Policy Configuration

 In SOC lab forest, change Audit Policy . To see all events that related with log in events, enabling "Logon/Logoff" audit events for telemetry generation.

![[Pasted image 20260426212812.png]]


### Step - 7. Client Side: DNS & IP Setup

Pointing the workstation to the DC for name resolution. 

   ![[Pasted image 20260426213304.png]]

### Step - 8. Domain Join Success

Successfully bridging the workstation and the controller.

   ![[Pasted image 20260426214541.png]]


### Step - 9. Final Session Verification

Proving that a domain user session is active and authenticated.

![[Pasted image 20260426215540.png]]
