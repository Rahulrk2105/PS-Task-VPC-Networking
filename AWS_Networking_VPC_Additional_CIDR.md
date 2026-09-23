# 🌐 AWS Networking – VPC & Additional CIDR

![AWS](https://img.shields.io/badge/AWS-Cloud-orange?logo=amazon-aws)
![Amazon VPC](https://img.shields.io/badge/Amazon-VPC-blue?logo=amazon-aws)
![Secondary CIDR](https://img.shields.io/badge/Secondary-CIDR-blue?logo=amazon-aws)


---

## 📌 Overview


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

<img width="1587" height="487" alt="image" src="https://github.com/user-attachments/assets/35c8fba7-ff09-4614-a78b-e15cceb1f216" />


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

<img width="1587" height="742" alt="image" src="https://github.com/user-attachments/assets/0ce296c7-ecfb-489d-9724-981faf375273" />

---

## 🛣️ Route Table

The VPC route table was verified with the following local routes:

```text
10.0.0.0/16 → local
10.1.0.0/16 → local
```

### 📸 Route Table

<img width="1600" height="721" alt="image" src="https://github.com/user-attachments/assets/1241c18b-b77a-4c09-8aa5-52a44348c6e9" />

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

The Amazon VPC was successfully created with the primary CIDR `10.0.0.0/16`.  
A secondary CIDR `10.1.0.0/16` was also added and verified through the VPC route table.
