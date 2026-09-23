# 🌐 AWS Networking – VPC & Additional CIDR

![AWS](https://img.shields.io/badge/AWS-Cloud-orange?logo=amazon-aws)
![Amazon VPC](https://img.shields.io/badge/Amazon-VPC-blue?logo=amazon-aws)
![Secondary CIDR](https://img.shields.io/badge/Secondary-CIDR-blue?logo=amazon-aws)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)

---

## 📌 Overview

This lab covers two AWS networking tasks:

1. **Create an Amazon VPC**
2. **Add Additional CIDR Blocks to an Amazon VPC**

---

## 🏠 Task 1 – Create an Amazon VPC

### Configuration

| Setting | Value |
|---|---|
| VPC Name | `Ps-task-vpc` |
| Region | `ap-south-1 (Mumbai)` |
| IPv4 CIDR | `10.0.0.0/16` |
| DNS Resolution | Enabled |
| DNS Hostnames | Enabled |

### Steps

```text
VPC
→ Your VPCs
→ Create VPC
→ VPC only
→ Name: Ps-task-vpc
→ IPv4 CIDR: 10.0.0.0/16
→ Create VPC
```

### 📸 VPC Details

![VPC Details](./screenshots/01-vpc-details.png)

---

## 🧩 Task 2 – Add Additional CIDR Blocks

### Configuration

| Setting | Value |
|---|---|
| Primary CIDR | `10.0.0.0/16` |
| Secondary CIDR | `10.1.0.0/16` |

### Steps

```text
VPC
→ Your VPCs
→ Ps-task-vpc
→ Actions
→ Edit CIDRs
→ Add new IPv4 CIDR
→ 10.1.0.0/16
```

### 📸 Secondary CIDR

![Secondary CIDR](./screenshots/02-secondary-cidr.png)

### 📸 VPC CIDRs

![VPC CIDRs](./screenshots/03-vpc-cidrs.png)

---

## 🛣️ Route Table

The VPC route table was verified with the following local routes:

```text
10.0.0.0/16 → local
10.1.0.0/16 → local
```

### 📸 Route Table

![Route Table](./screenshots/04-route-table.png)

---

## 🗺️ Network Configuration

```text
                 Ps-task-vpc
                10.0.0.0/16
                     │
          ┌──────────┴──────────┐
          │                     │
  Primary CIDR          Secondary CIDR
  10.0.0.0/16            10.1.0.0/16
```

---

## 📊 Final Verification

| Configuration | Status |
|---|---|
| VPC Created | ✅ |
| Primary CIDR `10.0.0.0/16` | ✅ |
| DNS Resolution | ✅ |
| DNS Hostnames | ✅ |
| Secondary CIDR `10.1.0.0/16` | ✅ |
| Route Table Verified | ✅ |
| Network Reachability | ⏳ |

> End-to-end network reachability was not tested because no EC2 test resources were created for this lab.

---

## 🧠 What I Learned

- Creating an Amazon VPC
- Configuring IPv4 CIDR blocks
- Enabling DNS Resolution and DNS Hostnames
- Adding a secondary CIDR block
- Verifying local VPC routes
- Understanding VPC address space expansion

---

## ✅ Conclusion

The Amazon VPC was successfully created with the primary CIDR `10.0.0.0/16`.  
A secondary CIDR `10.1.0.0/16` was also added and verified through the VPC route table.
