# Day 10 – VLAN Trunking Between Switches

## 📌 Objective
To establish **VLAN trunking between multiple switches** so that **same VLAN devices can communicate across different switches**, while **different VLANs remain isolated**.

---

## 🧰 Tools & Requirements
- Cisco Packet Tracer
- 3 × Cisco 2960 Switches
- 9 × End Devices (PCs)
- Straight-through Cables (PC to Switch)
- Cross-over Cables (Switch to Switch)

---

## 🗂️ Network Topology

![VLAN Trunking Topology](image.png)

---

## 🧱 VLAN Design

| VLAN ID | VLAN Name |
|------|----------|
| 2 | VLAN 2 |
| 3 | VLAN 3 |
| 4 | VLAN 4 |

---

## 🌐 IP Addressing Scheme  
(All devices are in **192.168.1.0/24** network for VLAN testing)

### 🔹 VLAN 2

| Device | IP Address |
|------|-----------|
| PC-PT | 192.168.1.1 |
| PC-PT | 192.168.1.4 |
| PC-PT | 192.168.1.7 |

---

### 🔹 VLAN 3

| Device | IP Address |
|------|-----------|
| PC-PT | 192.168.1.2 |
| PC-PT | 192.168.1.5 |
| PC-PT | 192.168.1.8 |

---

### 🔹 VLAN 4

| Device | IP Address |
|------|-----------|
| PC-PT | 192.168.1.3 |
| PC-PT | 192.168.1.6 |
| PC-PT | 192.168.1.9 |

---

## ⚙️ Switch Configuration

### 🔹 Step 1: Create VLANs (On All Switches)

```bash
enable
configure terminal

vlan 2
name VLAN2
exit

vlan 3
name VLAN3
exit

vlan 4
name VLAN4
exit
```
### 🔹 Step 2: Assign Access Ports

```bash
interface range fastEthernet 0/1 - 0/3
switchport mode access
switchport access vlan 2
exit

interface range fastEthernet 0/4 - 0/6
switchport mode access
switchport access vlan 3
exit

interface range fastEthernet 0/7 - 0/9
switchport mode access
switchport access vlan 4
exit
```

### 🔹 Step 3: Configure Trunk Ports (Between Switches)

```bash
interface range fastEthernet 0/23 - 0/24
switchport mode trunk
exit
```
- Repeat trunk configuration on all inter-switch links.

### 🧪 Testing & Verification

- ✅ Same VLAN Communication (Successful)
```bash
ping 192.168.1.7
```
- ✔ VLAN 2 devices can communicate across switches.

### ❌ Different VLAN Communication (Blocked)
```bash
ping 192.168.1.8
```
- ✖ Ping fails (Expected behavior – VLAN isolation)

### 📊 Result

- Same VLAN devices communicate across multiple switches
- Different VLAN devices cannot communicate
- Trunk links successfully carry multiple VLANs
- VLAN segmentation works as expected

### 🧠 Key Learning Outcomes

- Understood VLAN trunking concept
- Configured trunk ports between switches
- Verified VLAN isolation
- Learned real-world campus network behavior

### 👨‍💻 Author

- Abhishek Pundir
- B.Tech | Networking & CCNA Aspirant
- 30 Days of Cisco Packet Tracer Challenge 🚀
