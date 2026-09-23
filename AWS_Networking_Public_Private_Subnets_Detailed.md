# 🌐 Lab – Create Public and Private Subnets

![AWS](https://img.shields.io/badge/AWS-Cloud-orange?logo=amazon-aws)
![Amazon VPC](https://img.shields.io/badge/Amazon-VPC-blue?logo=amazon-aws)
![Public Subnet](https://img.shields.io/badge/Subnet-Public-green?logo=amazon-aws)
![Private Subnet](https://img.shields.io/badge/Subnet-Private-purple?logo=amazon-aws)
![Route Tables](https://img.shields.io/badge/Route-Tables-orange?logo=amazon-aws)

---

# 📖 Project Overview

In this hands-on lab, I created **Public Subnets** and **Private Subnets** inside the existing Amazon VPC.

I configured the subnet associations and public IP address settings based on the subnet type.

The lab covered:

- Public Subnets
- Private Subnets
- Availability Zones
- IPv4 CIDR Blocks
- Route Tables
- Route Table Associations
- Public IPv4 Address Assignment
- Private Subnet Configuration
- Auto-assign Public IPv4 Address
- Internet Gateway route for public connectivity

---

# 🏗️ Existing VPC

The subnets were created inside the existing VPC:

```text
VPC: Ps-task-vpc
Primary CIDR: 10.0.0.0/16
Secondary CIDR: 10.1.0.0/16
Region: ap-south-1 (Mumbai)
```

The VPC already had DNS Resolution and DNS Hostnames enabled.

---

# 🔹 Step 1 – Create Public Subnets

I created the required **Public Subnets** inside the VPC.

A public subnet is a subnet that uses a route table with a route to an **Internet Gateway**.

### Public Subnet Configuration

```text
VPC
    |
    └── Public Subnet
            |
            └── Public Route Table
                    |
                    └── Internet Gateway
```

The public subnet was configured with:

- VPC association
- Availability Zone
- IPv4 CIDR block
- Public Route Table
- Auto-assign Public IPv4 Address

### 📸 Screenshot

![Public Subnet](./screenshots/01-public-subnet.png)

---

# 🔹 Step 2 – Associate Public Route Table

After creating the Public Subnet, I associated it with the appropriate **Route Table**.

### Route Table Association

```text
Public Subnet
      |
      ↓
Public Route Table
      |
      ↓
Internet Gateway
```

The route table is used to control how traffic from the public subnet is routed.

### Public Route

```text
Destination: 0.0.0.0/0
Target: Internet Gateway
```

The `0.0.0.0/0` route represents the default IPv4 route.

### 📸 Screenshot

![Public Route Table](./screenshots/02-public-route-table.png)

---

# 🔹 Step 3 – Configure Public IP Assignment

For the Public Subnet, I configured **Auto-assign Public IPv4 Address**.

### Configuration

```text
Auto-assign Public IPv4 Address
→ Enabled
```

This allows resources launched in the subnet to automatically receive a public IPv4 address when the instance configuration allows it.

### 📸 Screenshot

![Public IP Assignment](./screenshots/03-public-ip-assignment.png)

---

# 🔹 Step 4 – Create Private Subnets

I created the required **Private Subnets** inside the same VPC.

A private subnet does not provide direct internet access through an Internet Gateway.

### Private Subnet Configuration

```text
VPC
    |
    └── Private Subnet
            |
            └── Private Route Table
```

The private subnet was configured with:

- VPC association
- Availability Zone
- IPv4 CIDR block
- Private Route Table
- Public IPv4 address assignment disabled

### 📸 Screenshot

![Private Subnet](./screenshots/04-private-subnet.png)

---

# 🔹 Step 5 – Associate Private Route Table

I associated the Private Subnet with the appropriate **Private Route Table**.

### Route Table Association

```text
Private Subnet
      |
      ↓
Private Route Table
```

The route table association determines which routes are applied to resources inside the private subnet.

### 📸 Screenshot

![Private Route Table](./screenshots/05-private-route-table.png)

---

# 🔹 Step 6 – Disable Public IP Assignment

For the Private Subnet, I disabled **Auto-assign Public IPv4 Address**.

### Configuration

```text
Auto-assign Public IPv4 Address
→ Disabled
```

This keeps resources launched in the private subnet from automatically receiving public IPv4 addresses.

### 📸 Screenshot

![Private IP Assignment](./screenshots/06-private-ip-assignment.png)

---

# 🔹 Step 7 – Public and Private Subnet Layout

The subnet configuration can be represented as:

```text
                         Ps-task-vpc
                              |
                ┌─────────────┴─────────────┐
                |                           |
                ↓                           ↓
          Public Subnets              Private Subnets
                |                           |
                ↓                           ↓
       Public Route Table          Private Route Table
                |                           |
                ↓                           |
        Internet Gateway                   |
                |                           |
                ↓                           |
        Internet Connectivity        No Public IP
```

---

# 🔍 Public vs Private Subnet

| Configuration | Public Subnet | Private Subnet |
|---|---|---|
| Route Table | Public Route Table | Private Route Table |
| Internet Gateway Route | Yes | No direct IGW route |
| Auto-assign Public IPv4 | Enabled | Disabled |
| Public IPv4 Address | Allowed | Not automatically assigned |
| Purpose | Public-facing resources | Internal/private resources |

---

# 🧠 AWS Networking Terms Used

## VPC

A **Virtual Private Cloud (VPC)** is the isolated virtual network where the subnets are created.

## Subnet

A **Subnet** is a logical section of a VPC IP address range.

## Public Subnet

A **Public Subnet** is associated with a route table that has a route to an **Internet Gateway**.

## Private Subnet

A **Private Subnet** does not have a direct route to an Internet Gateway.

## Route Table

A **Route Table** contains routing rules that control where network traffic is sent.

## Route Table Association

A **Route Table Association** connects a subnet to a route table.

## Internet Gateway

An **Internet Gateway** provides a path between a VPC and the internet when the appropriate route and public addressing are configured.

## Auto-assign Public IPv4 Address

This subnet setting controls whether launched resources can automatically receive a public IPv4 address.

## Availability Zone

An **Availability Zone (AZ)** is an isolated location within an AWS Region where subnets can be created.

## CIDR Block

A **CIDR Block** defines the IP address range assigned to the subnet.

---

# 📝 Important Notes

- Public and private subnets are created inside a VPC.
- Each subnet is associated with a route table.
- A public subnet uses a route to an Internet Gateway for public connectivity.
- Public IP assignment is enabled for the public subnet.
- Public IP assignment is disabled for the private subnet.
- Route table association determines the routing rules applied to each subnet.
