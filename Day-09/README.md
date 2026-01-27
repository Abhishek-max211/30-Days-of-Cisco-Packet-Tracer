# Day 09 – Inter-VLAN Routing (Router-on-a-Stick)

## 📌 Objective
To configure **Inter-VLAN Routing using Router-on-a-Stick** so that devices in **different VLANs can communicate** through a router.

---

## 🧰 Tools & Requirements
- Cisco Packet Tracer
- 1 × Router (ISR 4331)
- 1 × Switch (Cisco 2960)
- 6 × End Devices (PCs & Laptops)
- Straight-through Ethernet Cables

---

## 🗂️ Network Topology

![Network Topology](image.png)

---

## 🧱 VLAN Design

| VLAN ID | VLAN Name | Network |
|------|----------|----------|
| 2 | ADMIN | 192.168.1.0 /24 |
| 3 | STUDENTS | 192.168.2.0 /24 |

---

## 🌐 IP Address Configuration

### 🔹 VLAN 2 – ADMIN (192.168.1.0/24)

| Device | IP Address | Default Gateway |
|------|-----------|----------------|
| PC-PT | 192.168.1.2 | 192.168.1.1 |
| PC-PT | 192.168.1.3 | 192.168.1.1 |
| PC-PT | 192.168.1.4 | 192.168.1.1 |

---

### 🔹 VLAN 3 – STUDENTS (192.168.2.0/24)

| Device | IP Address | Default Gateway |
|------|-----------|----------------|
| Laptop-PT | 192.168.2.2 | 192.168.2.1 |
| Laptop-PT | 192.168.2.3 | 192.168.2.1 |
| Laptop-PT | 192.168.2.4 | 192.168.2.1 |

---

## ⚙️ Switch Configuration (VLAN & Trunk)

```bash
enable
configure terminal

vlan 2
name ADMIN
exit

vlan 3
name STUDENTS
exit

interface range fastEthernet 0/1 - 0/3
switchport mode access
switchport access vlan 2
exit

interface range fastEthernet 0/4 - 0/6
switchport mode access
switchport access vlan 3
exit

interface fastEthernet 0/24
switchport mode trunk
exit

end
write memory
```

### ⚙️ Router Configuration (Router-on-a-Stick)

```bash
enable
configure terminal

interface g0/0/0
no shutdown
exit

interface g0/0/0.1
encapsulation dot1Q 2
ip address 192.168.1.1 255.255.255.0
exit

interface g0/0/0.2
encapsulation dot1Q 3
ip address 192.168.2.1 255.255.255.0
exit

end
write memory
```
### 🧪 Testing & Verification

```bash
ping 192.168.2.2
ping 192.168.1.4
```

- ✔ Successful ping between VLAN 2 and VLAN 3
- ✔ Inter-VLAN routing is working correctly

### 📊 Result

- Devices in different VLANs can communicate
- Router successfully routes traffic using sub-interfaces
- Router-on-a-Stick configuration completed successfully

### 🧠 Key Learning Outcomes

- Understood Inter-VLAN Routing
- Configured Router-on-a-Stick
- Used sub-interfaces with dot1Q encapsulation
- Verified routing using ICMP ping

 ### 👨‍💻 Author

- Abhishek Pundir
- B.Tech | Networking & CCNA Aspirant
- 30 Days of Cisco Packet Tracer Challenge 🚀
