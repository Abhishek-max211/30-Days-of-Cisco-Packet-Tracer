# 🌐 Static Routing Between 4 Routers | Cisco Packet Tracer

![Network Topology](image.png)

---

## 📌 Project Overview
This project demonstrates **Static Routing between four routers** using Cisco Packet Tracer.  
Each router connects to its own **LAN**, and all four networks communicate with each other using **manually configured static routes**.

This lab strengthens core **CCNA routing concepts**, including:
- Router-to-router communication
- Serial DCE connections
- Static route configuration
- End-to-end connectivity testing

---

## 🎯 Objectives
- Enable static routing between 4 routers
- Allow 4 different networks to communicate
- Configure serial and Ethernet interfaces
- Assign default gateways for end devices
- Verify connectivity using ICMP (ping)

---

## 🧰 Network Requirements
- 4 × Routers (ISR 4331)
- 4 × Switches (Cisco 2960)
- 8 × End Devices (PCs)
- Copper Straight-Through cables (LAN)
- Serial DCE cables (Router-to-Router)

---

## 🗺️ Network Topology Summary

| Router | LAN Network | Default Gateway |
|------|------------|-----------------|
| Router0 | 192.168.1.0/24 | 192.168.1.1 |
| Router1 | 192.168.2.0/24 | 192.168.2.1 |
| Router2 | 192.168.3.0/24 | 192.168.3.1 |
| Router3 | 192.168.4.0/24 | 192.168.4.1 |

---

## 🖥️ IP Addressing Scheme

### 🔹 LAN 1 – Router0
- Router0: `192.168.1.1`
- PC1: `192.168.1.2`
- PC2: `192.168.1.3`

### 🔹 LAN 2 – Router1
- Router1: `192.168.2.1`
- PC3: `192.168.2.2`
- PC4: `192.168.2.3`

### 🔹 LAN 3 – Router2
- Router2: `192.168.3.1`
- PC5: `192.168.3.2`
- PC6: `192.168.3.3`

### 🔹 LAN 4 – Router3
- Router3: `192.168.4.1`
- PC7: `192.168.4.2`
- PC8: `192.168.4.3`

---

## 🔗 Serial Link Networks

| Link | Network |
|----|--------|
| Router0 ↔ Router1 | 192.168.5.0/30 |
| Router1 ↔ Router2 | 192.168.6.0/30 |
| Router2 ↔ Router3 | 192.168.7.0/30 |

---

## ⚙️ Router Configuration

### 🔹 Router0
```bash
enable
configure terminal
hostname Reborn1

interface g0/0/0
 ip address 192.168.1.1 255.255.255.0
 no shutdown

interface s0/0/0
 ip address 192.168.5.1 255.255.255.252
 clock rate 64000
 no shutdown

ip route 192.168.2.0 255.255.255.0 192.168.5.2
ip route 192.168.3.0 255.255.255.0 192.168.5.2
ip route 192.168.4.0 255.255.255.0 192.168.5.2
```
### 🔹 Router1
```bash
hostname Reborn2

interface g0/0/0
 ip address 192.168.2.1 255.255.255.0
 no shutdown

interface s0/0/0
 ip address 192.168.5.2 255.255.255.252
 no shutdown

interface s0/0/1
 ip address 192.168.6.1 255.255.255.252
 clock rate 64000
 no shutdown

ip route 192.168.1.0 255.255.255.0 192.168.5.1
ip route 192.168.3.0 255.255.255.0 192.168.6.2
ip route 192.168.4.0 255.255.255.0 192.168.6.2
```

### 🔹 Router2
```bash
hostname Reborn3

interface g0/0/0
 ip address 192.168.3.1 255.255.255.0
 no shutdown

interface s0/0/0
 ip address 192.168.6.2 255.255.255.252
 no shutdown

interface s0/0/1
 ip address 192.168.7.1 255.255.255.252
 clock rate 64000
 no shutdown

ip route 192.168.1.0 255.255.255.0 192.168.6.1
ip route 192.168.2.0 255.255.255.0 192.168.6.1
ip route 192.168.4.0 255.255.255.0 192.168.7.2
```

### 🔹 Router3
```bash
hostname Reborn4

interface g0/0/0
 ip address 192.168.4.1 255.255.255.0
 no shutdown

interface s0/0/0
 ip address 192.168.7.2 255.255.255.252
 no shutdown

ip route 192.168.1.0 255.255.255.0 192.168.7.1
ip route 192.168.2.0 255.255.255.0 192.168.7.1
ip route 192.168.3.0 255.255.255.0 192.168.7.1
```

### Verification
- Ping tested between all PCs across networks
- Router-to-router ICMP successful
- End-to-end connectivity confirmed

### 📚 Key Concepts Learned
Static Routing

- Serial DCE configuration
- Multiple network routing
- Default gateway usage
- Troubleshooting ICMP failures

### 🚀 Future Enhancements

- Replace static routing with RIP / OSPF
- Add redundancy
- Implement ACLs
- Configure DHCP

### 🧑‍💻 Author

- Abhishek Pundir
- B.Tech | Networking | CCNA Aspirant
