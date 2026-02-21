# 🔐 Extended ACL Configuration – Cisco Packet Tracer Lab

## 📌 Objective
To configure and verify an **Extended Access Control List (ACL)** in Cisco Packet Tracer to block HR Department from accessing the Server Network while allowing IT Department access.

---

## 🖼️ Network Topology

![Extended ACL Topology](image.png)

---

## 🏗️ Lab Requirements

- 1 Router (ISR 4331)
- 2 Switches (2960-24TT)
- 2 Servers
- 4 Client PCs
- Straight-through cables
- Cisco Packet Tracer

---

## 🌐 IP Addressing Scheme

### 🔹 LAN Network – 192.168.1.0/24

| Department | Device | IP Address | Default Gateway |
|------------|--------|------------|----------------|
| IT Dept | PC1 | 192.168.1.2 | 192.168.1.1 |
| IT Dept | PC2 | 192.168.1.3 | 192.168.1.1 |
| HR Dept | PC3 | 192.168.1.4 | 192.168.1.1 |
| HR Dept | PC4 | 192.168.1.5 | 192.168.1.1 |

### 🔹 Server Network – 192.168.2.0/24

| Device | IP Address | Default Gateway |
|--------|------------|----------------|
| Server1 | 192.168.2.2 | 192.168.2.1 |
| Server2 | 192.168.2.3 | 192.168.2.1 |

---

## 🛣️ Router Configuration

### Step 1️⃣ Configure Interfaces

```
enable
configure terminal

interface g0/0/0
ip address 192.168.1.1 255.255.255.0
no shutdown
exit

interface g0/0/1
ip address 192.168.2.1 255.255.255.0
no shutdown
exit
```

---

## 🔒 Extended ACL Configuration

### 🎯 Scenario
Block HR Department (192.168.1.4 & 192.168.1.5) from accessing Server Network (192.168.2.0/24)  
Allow IT Department to access servers.

---

### Step 2️⃣ Create Extended ACL

```
access-list 100 deny ip host 192.168.1.4 192.168.2.0 0.0.0.255
access-list 100 deny ip host 192.168.1.5 192.168.2.0 0.0.0.255
access-list 100 permit ip any any
```

---

### Step 3️⃣ Apply ACL to Interface

👉 Extended ACL should be placed **close to the source**.

```
interface g0/0/0
ip access-group 100 in
exit
```

---

## 🧪 Testing & Verification

### ❌ From HR PC (192.168.1.4 / 192.168.1.5)

```
ping 192.168.2.2
ping 192.168.2.3
```

Expected Result:
```
Destination host unreachable
Packets: Sent = 4, Received = 0, Lost = 4 (100% loss)
```

---

### ✅ From IT PC (192.168.1.2 / 192.168.1.3)

```
ping 192.168.2.2
ping 192.168.2.3
```

Expected Result:
```
Reply from 192.168.2.2
Reply from 192.168.2.3
```

---

## 📊 Result Summary

| Source | Destination | Result |
|--------|------------|--------|
| HR PCs | Server Network | ❌ Denied |
| IT PCs | Server Network | ✅ Allowed |

---

## 📚 Concepts Covered

- Extended ACL (100–199)
- Source & Destination filtering
- Wildcard masks
- ACL placement rules
- Inbound vs Outbound filtering
- Implicit deny rule
- Traffic testing using Ping

---

## 🔎 Why Extended ACL?

Unlike Standard ACL, Extended ACL allows filtering based on:
- Source IP
- Destination IP
- Protocol (IP, TCP, UDP, ICMP)
- Port numbers

This provides more granular traffic control.

---

## 📁 Project Structure

```
Extended-ACL-Lab/
│
├── README.md
├── image.png
└── Extended-ACL Configuration.pkt
```

---

## 👨‍💻 Author

**Abhishek Pundir**  
Engineering Student | Networking Enthusiast | CCNA Aspirant  

---

## 🚀 Learning Outcome

✔ Implemented traffic filtering using Extended ACL  
✔ Understood ACL placement best practices  
✔ Verified traffic blocking using simulation mode  
✔ Gained practical CCNA-level ACL experience  

---

⭐ If you found this helpful, consider starring the repository!
