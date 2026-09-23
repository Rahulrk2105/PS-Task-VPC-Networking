# 🌐 Public and Private Subnets

![AWS](https://img.shields.io/badge/AWS-Cloud-orange?logo=amazon-aws)
![Amazon VPC](https://img.shields.io/badge/Amazon-VPC-blue?logo=amazon-aws)
![Public Subnet](https://img.shields.io/badge/Subnet-Public-green?logo=amazon-aws)
![Private Subnet](https://img.shields.io/badge/Subnet-Private-purple?logo=amazon-aws)
![Route Tables](https://img.shields.io/badge/Route-Tables-orange?logo=amazon-aws)


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

<img width="1577" height="652" alt="image" src="https://github.com/user-attachments/assets/6eb60fc1-0007-4b95-990e-5d1c88b8a665" />


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

<img width="1601" height="737" alt="image" src="https://github.com/user-attachments/assets/076addfb-9e3a-409e-b43f-22dd2195b947" />


---

# 🔹 Step 3 – Configure Public IP Assignment

For the Public Subnet, I configured **Auto-assign Public IPv4 Address**.

### Configuration

```text
Auto-assign Public IPv4 Address
→ Enabled
```

This allows resources launched in the subnet to automatically receive a public IPv4 address when the instance configuration allows it.


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

<img width="1585" height="692" alt="image" src="https://github.com/user-attachments/assets/6bdefb0a-b118-42ff-a9d2-4bcc918616db" />

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

<img width="1586" height="576" alt="image" src="https://github.com/user-attachments/assets/172eab69-6774-4311-a72b-9c995aec9710" />

---

# 🔹 Step 6 – Disable Public IP Assignment

For the Private Subnet, I disabled **Auto-assign Public IPv4 Address**.

### Configuration

```text
Auto-assign Public IPv4 Address
→ Disabled
```

This keeps resources launched in the private subnet from automatically receiving public IPv4 addresses.


---

# 🔹 Step 7 – Create Isolated Subnets

I created the required **Isolated Subnets** inside the VPC.

An isolated subnet does not have a route to an **Internet Gateway** or other external network.

### Isolated Subnet Configuration

```text
VPC
    |
    └── Isolated Subnet
            |
            └── Isolated Route Table
```

The isolated subnet was configured with:

- VPC association
- Availability Zone
- IPv4 CIDR block
- Isolated Route Table
- No Internet Gateway route
- Public IPv4 address assignment disabled

### 📸 Screenshot

<img width="1592" height="655" alt="image" src="https://github.com/user-attachments/assets/66afcf84-6f05-4622-aa83-f018d32372d3" />


---

# 🔹 Step 8 – Associate Isolated Route Table

I associated the Isolated Subnet with the appropriate **Route Table**.

```text
Isolated Subnet
      |
      ↓
Isolated Route Table
```

The isolated route table does not contain a default route to an Internet Gateway.

### Route Configuration

```text
Destination: VPC CIDR
Target: local
```

### 📸 Screenshot

<img width="1607" height="735" alt="image" src="https://github.com/user-attachments/assets/b1fa56db-d83a-40c6-8d21-da8fd9d0a51b" />


---

# 🔹 Step 9 – Validate Subnet Isolation

I checked the route table associated with the Isolated Subnet to confirm that there was no route to an **Internet Gateway**.

```text
Isolated Subnet
      |
      ↓
Isolated Route Table
      |
      └── No Internet Gateway Route
```

This keeps resources inside the isolated subnet from having direct internet connectivity.


---

# 🔍 Isolated Subnet Configuration

| Configuration | Isolated Subnet |
|---|---|
| Route Table | Isolated Route Table |
| Internet Gateway Route | No |
| Public IPv4 Assignment | Disabled |
| External Connectivity | Isolated |
| Purpose | Resources requiring network isolation |

---

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

