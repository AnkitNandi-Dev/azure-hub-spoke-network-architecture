
# Secure Hub-Spoke Network Architecture in Azure

## Project Overview
This project demonstrates the implementation of a **secure hub-spoke network architecture** using Microsoft Azure. The design focuses on centralized network security, segmented application tiers, and secure administrative access.

The architecture consists of a **hub virtual network hosting shared infrastructure services** and a **spoke virtual network hosting application workloads**. Traffic from the spoke network is routed through a centralized firewall for inspection and control.

This project reflects a **common enterprise cloud networking pattern used in production environments**.

---

# Architecture Diagram

![Architecture Diagram](screenshots/architecture-diagram.png)

---

# Cloud Services Used

This architecture uses the following Azure services:

- Microsoft Azure
- Azure Virtual Network
- Azure Firewall
- Azure Bastion
- Network Security Groups (NSG)
- Azure Route Tables
- Azure Virtual Machines

---

# Network Architecture

## Hub Network

The **Hub Virtual Network** hosts shared infrastructure components used across the environment.

Components deployed in the hub:

- Azure Firewall
- Azure Bastion
- AzureFirewallSubnet
- AzureBastionSubnet

Purpose of the hub network:

- Centralized traffic inspection
- Secure administrative access
- Shared networking services

---

## Spoke Network

The **Spoke Virtual Network** hosts the application workloads.

Components deployed in the spoke:

- Web tier subnet
- API tier subnet
- Virtual machines for application layers

This design allows application resources to remain **isolated while still using shared security services from the hub**.

---

# Traffic Flow

Traffic between the internet and application workloads follows a controlled path:

Internet  
↓  
Azure Firewall  
↓  
Hub Virtual Network  
↓  
VNet Peering  
↓  
Spoke Virtual Network  
↓  
Web Tier → API Tier  

Outbound traffic from the spoke network is routed through the firewall using a **route table with destination 0.0.0.0/0**.

---

# Security Implementation

## Network Segmentation

The application environment is divided into separate subnets:

- Web Tier
- API Tier

This separation reduces security risks and allows controlled communication between tiers.

---

## Network Security Groups

Network Security Groups were applied at the subnet level to enforce traffic rules.

Examples of rules implemented:

- Allow HTTP/HTTPS traffic to the web tier
- Restrict direct access to the API tier
- Deny all other unauthorized traffic

---

## Azure Firewall

Azure Firewall is deployed in the hub network to provide **centralized traffic inspection and filtering**.

Firewall capabilities used:

- Network rules controlling outbound internet access
- Centralized security control for spoke networks

---

# Secure Administrative Access

Administrative access to virtual machines is provided through **Azure Bastion**.

Benefits:

- No public IP addresses assigned to VMs
- Secure SSH/RDP access through the Azure portal
- Reduced attack surface

---

# Forced Tunneling with Route Tables

Outbound traffic from the spoke network is forced through the firewall using a route table.

Configuration:

Destination:
0.0.0.0/0

Next hop:
Azure Firewall private IP

This ensures all outbound traffic is inspected before leaving the network.

---

# Screenshots

## Resource Architecture

![Resource Visualizer](screenshots/resource-visualizer.png)

---

## VNet Peering Configuration

![VNet Peering](screenshots/vnet-peering.png)

---

## Azure Firewall Rules

![Firewall Rules](screenshots/firewall-rules.png)

---

## Network Security Group Rules

![NSG Rules](screenshots/nsg-rules.png)

---

## Route Table Configuration

![Route Table](screenshots/route-table.png)

---

# Key Learnings

- Implemented a hub-spoke network topology in Azure
- Configured centralized firewall inspection
- Applied subnet segmentation using Network Security Groups
- Implemented forced tunneling using route tables
- Enabled secure VM access using Azure Bastion

---

# Future Improvements

Possible enhancements for a production environment:

- Implement Azure Load Balancer for web tier
- Deploy Virtual Machine Scale Sets for auto scaling
- Enable centralized logging using Azure Monitor
- Use Application Security Groups for simplified NSG rules

---

# Project Outcome

This project demonstrates how Azure networking services can be combined to create a **secure, scalable, and well-structured cloud network architecture** following enterprise design principles.

---

# Author

Ankit  
Cloud Networking Project – Azure
