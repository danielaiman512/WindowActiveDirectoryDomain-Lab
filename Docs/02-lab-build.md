
# Lab 1 — Windows Server Active Directory Environment

## Project Overview

This project demonstrates the deployment of a small Windows-based domain environment using Windows Server 2025 and Windows 11 Pro.

The lab simulates a basic business network in which a Windows Server domain controller provides centralized identity management and DNS services. A Windows 11 client is connected to the domain to demonstrate how a workstation participates in an Active Directory environment.

The project was designed to develop and demonstrate foundational IT support and system administration skills, including:

- Windows Server configuration
- Active Directory Domain Services (AD DS)
- DNS configuration and troubleshooting
- Domain joining and authentication
- Network configuration
- User and computer account management
- Technical documentation and evidence collection

## Lab Objectives

The primary objectives of this lab were to:

1. Deploy a Windows Server domain controller.
2. Configure a static IPv4 address for the server.
3. Install and configure Active Directory Domain Services.
4. Create an Active Directory domain.
5. Configure DNS for domain name resolution.
6. Configure a Windows 11 client on the same virtual network.
7. Join the client workstation to the domain.
8. Verify domain authentication and connectivity.

## Environment and Topology

The lab consists of two virtual machines connected through an isolated virtual network.

| Component | Configuration |
|---|---|
| Domain Controller | DC01 |
| Server Operating System | Windows Server 2025 |
| Client Workstation | CLIENT01 |
| Client Operating System | Windows 11 Pro |
| Domain Name | `company.com` |
| Virtual Network | `AD-LAB` |
| Network Type | Internal network |
| IPv4 Subnet | `10.0.0.0/24` |

### Network Configuration

| Device | IPv4 Address | Subnet Mask | DNS Server |
|---|---|---|---|
| DC01 | `10.0.0.1` | `255.255.255.0` | `127.0.0.1` |
| CLIENT01 | `10.0.0.2` | `255.255.255.0` | `10.0.0.1` |

The domain controller provides DNS resolution for the Active Directory domain. The client uses the domain controller as its DNS server so that it can locate domain services.

> **Note:** The configuration above represents the planned lab topology. Any differences in the final implementation should be documented here.

## Architecture

The environment follows a simple client-server architecture.

- **DC01:** Hosts Active Directory Domain Services and DNS.
- **CLIENT01:** Represents a domain-connected Windows workstation.
- **Active Directory:** Provides centralized identity and computer account management.
- **DNS:** Allows the client to resolve domain names and locate domain services.
- **AD-LAB:** Provides an isolated network for communication between the virtual machines.

## Implementation Summary

### 1. Virtual Machine Deployment

Two virtual machines were created for the lab:

- A Windows Server 2025 virtual machine named `DC01`
- A Windows 11 Pro virtual machine named `CLIENT01`



<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/5cd24fe2-5636-49b5-885a-565271447347" />

**Figure 1 — Virtual machine configuration and network assignment for Server.**

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/cd8e8f4a-8e2f-4629-862f-bf7002614a36" />

**Figure 2 — Virtual machine configuration and network assignment for Client.**

### 2. Domain Controller Configuration

The server was configured with a static IPv4 address to provide a consistent endpoint for domain services.

The server was assigned the hostname `DC01` and configured with the following address:

- IPv4 address: `10.0.0.1`
- Subnet mask: `255.255.255.0`
- Preferred DNS: `127.0.0.1`

Active Directory Domain Services was installed, and the server was promoted to a domain controller for the domain `company.com`.

<img width="1920" height="1080" alt="Promote to adds" src="https://github.com/user-attachments/assets/009594e1-242c-4430-8b23-49622629f7ce" />

**Figure 3 — Domain controller configuration.**

### 3. Active Directory and DNS

The Active Directory domain `company.com` was created to provide centralized identity management.

DNS was configured as part of the domain controller environment. The client workstation uses the domain controller's IP address for DNS resolution.

This configuration allows the workstation to locate domain services and communicate with the domain controller using the domain name.

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/2d27f17f-c9c2-460b-88fd-5564137486fa" />

**Figure 4 — Active Directory Users and Computers displaying the company.com domain.**

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/ca72aa9e-e62c-438f-a011-7d41e43a06f5" />
**Figure 4.1 — DNS Manager displaying the company.com forward lookup zone hosted on DC01. The zone provides name resolution for the Active Directory domain.**

### 4. Client Workstation Configuration

The Windows 11 workstation was configured with a static IPv4 address and the domain controller as its DNS server.

The workstation was assigned the hostname `CLIENT01`.

The client was then joined to the `company.com` domain.

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/3f724e22-59c8-4cf1-83f9-8a31069774f1" />

**Figure 5 — Windows 11 workstation joined to the domain.**

## Final Environment

The completed lab provides a basic centralized Windows domain environment.

The domain controller manages domain identities and provides DNS services, while the Windows 11 workstation demonstrates domain membership and centralized authentication.

This environment serves as a foundation for additional IT support and system administration scenarios, including:

- Creating and managing users and groups
- Organizational Unit (OU) design
- Group Policy configuration
- Password and account troubleshooting
- DNS troubleshooting
- Workstation access issues

## Project Status

**Status:** [Completed]

The implementation and validation status should reflect the actual state of the lab. Screenshots and verification results are maintained separately in the project evidence documentation.

## Skills Demonstrated

- Windows Server administration
- Active Directory Domain Services
- DNS fundamentals
- IPv4 configuration
- Windows client configuration
- Domain joining
- Technical documentation
- Virtual machine networking
