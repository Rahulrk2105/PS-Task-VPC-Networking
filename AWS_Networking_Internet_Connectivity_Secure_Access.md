# 🌐 Internet Gateway & Secure Internet Access NAT Gw

![AWS](https://img.shields.io/badge/AWS-Cloud-orange?logo=amazon-aws)
![Internet Gateway](https://img.shields.io/badge/Internet-Gateway-blue?logo=amazon-aws)
![NAT Gateway](https://img.shields.io/badge/NAT-Gateway-purple?logo=amazon-aws)
![Elastic IP](https://img.shields.io/badge/Elastic-IP-green?logo=amazon-aws)

---

# 🔹 Connect an Amazon VPC to the Internet

I configured internet connectivity for the VPC using an **Internet Gateway**.

### Configuration

- Internet Gateway
- VPC Attachment
- Public Route Table
- Default Route
- Internet-bound Traffic

### Internet Gateway

I created an **Internet Gateway** and attached it to the VPC.

```text
VPC
 |
 └── Internet Gateway
```

### 📸 Screenshot

<img width="1611" height="462" alt="image" src="https://github.com/user-attachments/assets/b39441b0-9114-4404-a23c-77469ff4b0b3" />


---

# 🔹 Configure Default Routes

I configured the default route in the public route table.

```text
Destination: 0.0.0.0/0
Target: Internet Gateway
```

This route allows internet-bound traffic from the public subnet to reach the Internet Gateway.

```text
Public Subnet
      |
      ↓
Public Route Table
      |
      ↓
0.0.0.0/0
      |
      ↓
Internet Gateway
      |
      ↓
Internet
```

### 📸 Screenshot

<img width="1580" height="367" alt="image" src="https://github.com/user-attachments/assets/b7bfb72d-c7d9-42d1-a62c-04f2f3e55ec1" />

---

# 🔹 Enable Secure Internet Access

I configured secure outbound internet access for resources in the private subnet using a **NAT Gateway**.

The configuration included:

- NAT Gateway
- Elastic IP Address
- Public Subnet
- Private Route Table
- Default Route

### NAT Gateway

I created a **NAT Gateway** in the public subnet and associated an **Elastic IP Address** with it.

```text
Private Subnet
      |
      ↓
Private Route Table
      |
      ↓
NAT Gateway
      |
      ↓
Internet Gateway
      |
      ↓
Internet
```

### 📸 Screenshot

<img width="1611" height="697" alt="image" src="https://github.com/user-attachments/assets/cdeda795-2b11-43e6-97f6-43f140196e5f" />


---

# 🔹 Allocate Elastic IP

I allocated an **Elastic IP Address** for the NAT Gateway.

The Elastic IP provides a static public IPv4 address for the NAT Gateway.

### 📸 Screenshot

<img width="1605" height="406" alt="image" src="https://github.com/user-attachments/assets/c423c2e1-d851-49a4-8eea-dcfe515ed55a" />


---

# 🔹 Configure Private Route Tables

I updated the private route table to send internet-bound traffic through the NAT Gateway.

```text
Destination: 0.0.0.0/0
Target: NAT Gateway
```

The traffic flow was:

```text
Private Resource
      |
      ↓
Private Route Table
      |
      ↓
0.0.0.0/0
      |
      ↓
NAT Gateway
      |
      ↓
Internet Gateway
      |
      ↓
Internet
```

### 📸 Screenshot

<img width="1586" height="497" alt="image" src="https://github.com/user-attachments/assets/22c45593-5b22-49d8-92a1-666d07b97d0d" />


---

## Internet Gateway

An **Internet Gateway (IGW)** provides a path between the VPC and the internet.

## Default Route

The default IPv4 route is:

```text
0.0.0.0/0
```

It matches traffic destined for addresses that are not covered by more specific routes.

## NAT Gateway

A **NAT Gateway** allows resources in a private subnet to initiate outbound connections to the internet without requiring public IPv4 addresses on those resources.

## Elastic IP

An **Elastic IP Address** is a static public IPv4 address that can be associated with AWS resources such as a NAT Gateway.

## Public Route Table

The public route table contains a default route to the **Internet Gateway**.

## Private Route Table

The private route table contains a default route to the **NAT Gateway** for outbound internet access.
