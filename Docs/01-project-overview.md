# Project Overview

## 1. Introduction

This project involves building a small Windows domain environment using Windows Server 2025 and Windows 11 Pro.

The environment represents a simplified business network where a central server manages user accounts, computers, and domain authentication.

I built this lab to understand how Active Directory works and how an IT support technician can manage and troubleshoot domain-connected computers.

## 2. Business Scenario

A small company needs a centralized system for managing employee accounts and Windows computers.

Instead of maintaining separate local accounts on every workstation, the company uses Active Directory to centrally manage user identities and domain membership.

In this lab, I simulate this environment by configuring:

- A Domain Controller named DC01.
- An Active Directory domain named company.com.
- A Windows workstation named CLIENT01.
- A domain user named helpdesk1.

The workstation is joined to the domain so that the domain user can authenticate using their Active Directory credentials.

## 3. Project Scope

### Included

- Windows Server 2025 installation
- Static IP configuration
- Active Directory Domain Services installation
- Domain Controller promotion
- DNS configuration
- Active Directory user creation
- Windows 11 domain joining
- Domain user authentication
- Basic network and DNS troubleshooting

### Not Included

- Production Active Directory deployment
- Multiple Domain Controllers
- Active Directory replication
- Microsoft Entra ID integration
- Group Policy deployment beyond default domain behavior
- Enterprise certificate services
- Production backup and disaster recovery

These topics can be explored in future projects.

## 4. Lab Environment

| Device | DC01 | CLIENT01 |
|---|---|---|
| Operating System | Windows Server 2025 | Windows 11 Pro |
| Hostname | DC01 | CLIENT01 |
| IPv4 Address | 10.0.0.1 | 10.0.0.2 |
| Subnet Mask | 255.255.255.0 | 255.255.255.0 |
| DNS Server | 127.0.0.1 | 10.0.0.1 |
| Domain | company.com | company.com |
| Role | Domain Controller | Domain Client |

## 5. Network Design

The network uses the private IPv4 subnet:

`10.0.0.0/24`

The subnet mask is:

`255.255.255.0`

The two virtual machines use static IP addresses.

DC01 provides DNS and Active Directory services to CLIENT01.

The client sends DNS queries to DC01 so it can locate the Domain Controller and other domain services.

### Why DNS is important

Active Directory depends on DNS to locate domain services.

If the client uses an incorrect DNS server, it may be unable to locate the Domain Controller even when the IP addresses are correctly configured.

For this reason, CLIENT01 uses 10.0.0.1 as its DNS server.

DC01 uses 127.0.0.1 as its DNS setting, which is the IPv4 loopback address and points back to the local machine.

## 6. Expected Outcome

At the end of the project:

- DC01 is functioning as a Domain Controller.
- The company.com domain exists.
- DNS is configured on DC01.
- The helpdesk1 account exists in Active Directory.
- CLIENT01 is joined to company.com.
- CLIENT01 can resolve the Domain Controller.
- helpdesk1 can sign in to CLIENT01 using domain credentials.

## 7. Project Safety

This environment is intended for educational use.

The virtual machines should use a private virtual network.

The lab should not expose Active Directory services directly to the public internet.

The domain user password should not be included in GitHub documentation or screenshots.
