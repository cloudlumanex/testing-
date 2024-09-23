
# testing-


# ShopEasy Azure Infrastructure

This repository contains the setup for a secure, scalable multi-tier application infrastructure for the retail company "ShopEasy" using Azure Virtual Network and other key Azure services.

## Project Overview

ShopEasy is expanding its online presence and requires a robust infrastructure to handle its growing customer base. This project implements the following components:

1. **Virtual Network with Subnets**
2. **Virtual Machines for Web, Application, and Database layers**
3. **Network Security Groups (NSGs) for traffic management**
4. **Bastion Host for secure VM access**
5. **Azure Load Balancer and Auto-Scaling for high availability**

## Table of Contents

- [Prerequisites](#prerequisites)
- [Step-by-Step Implementation](#step-by-step-implementation)
  - [1. Create a Virtual Network](#1-create-a-virtual-network)
  - [2. Deploy Virtual Machines](#2-deploy-virtual-machines)
  - [3. Implement Network Security](#3-implement-network-security)
  - [4. Enable Load Balancing and Auto-Scaling](#4-enable-load-balancing-and-auto-scaling)
- [Outcome](#outcome)

## Prerequisites

- Azure account with appropriate permissions to create resources.
- Basic knowledge of Azure services and networking concepts.

## Step-by-Step Implementation

### 1. Create a Virtual Network

1. Log in to the [Azure Portal](https://portal.azure.com/).
2. Navigate to **"Create a resource"** > **"Networking"** > **"Virtual Network"**.
3. Fill in the basic information:
   - **Name**: `ShopEasyVNet`
   - **Region**: Choose the desired Azure region.
   - **Address space**: `10.0.0.0/16`.
4. Click **Next** to go to the Subnet configuration.
5. Configure three subnets:
   - **Web Subnet**: `10.0.1.0/24`
   - **Application Subnet**: `10.0.2.0/24`
   - **Database Subnet**: `10.0.3.0/24`
6. Click **Review + Create** and then **Create**.

### 2. Deploy Virtual Machines

1. **Deploy Windows VM in the Web Subnet**:
   - Navigate to **"Create a resource"** > **"Compute"** > **"Windows Server"**.
   - Name it `ShopEasyWebVM` and place it in the Web Subnet.

2. **Deploy Linux VM in the Application Subnet**:
   - Repeat the steps, choosing a Linux image.
   - Name it `ShopEasyAppVM` and place it in the Application Subnet.

3. **Deploy SQL Server VM in the Database Subnet**:
   - Repeat the steps using a SQL Server image.
   - Name it `ShopEasyDBVM` and place it in the Database Subnet.

### 3. Implement Network Security

1. **Configure Network Security Groups (NSGs)**:
   - Go to **"Create a resource"** > **"Networking"** > **"Network Security Group"**.
   - Create an NSG for each subnet:
     - **Web NSG**: Allow HTTP (80) and HTTPS (443).
     - **Application NSG**: Allow traffic from Web NSG.
     - **Database NSG**: Allow traffic from Application NSG on port 1433.
   - Associate each NSG with its respective subnet.

2. **Set Up a Bastion Host**:
   - Go to **"Create a resource"** > **"Networking"** > **"Bastion"**.
   - Select `ShopEasyVNet` to allow secure access to VMs.

### 4. Enable Load Balancing and Auto-Scaling

1. **Deploy an Azure Load Balancer**:
   - Go to **"Create a resource"** > **"Networking"** > **"Load Balancer"**.
   - Fill in the details:
     - **Name**: `ShopEasyLoadBalancer`.
     - **Region**: Same as VNet.
     - **Type**: Public/Private as needed.
   - Configure frontend IP and backend pools (add Web VMs).

2. **Implement Auto-Scaling**:
   - Go to the Web VM scale set (or create one if necessary).
   - Configure scaling rules based on metrics (CPU usage, request count).
   - Define minimum and maximum instance counts.

## Outcome

By completing these steps, you will have a secure and scalable multi-tier application infrastructure for ShopEasy using Azure services. Ensure to review and test each component for proper functionality and security.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

