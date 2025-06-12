

# Secure and Scalable Enterprise Network – Cisco Packet Tracer



## 📘 Project Definition

**Secure and Scalable Enterprise Network Design** is a final-semester networking project built using **Cisco Packet Tracer**. It simulates a real-world enterprise network featuring departmental segmentation, secure access, dynamic routing, internet connectivity, and wireless support.

The network is designed to be:

* **Secure** – via SSH, ACLs, and port security
* **Scalable** – using OSPF and NAT for growth and external access
* **Automated** – with DHCP and DNS for dynamic IP and name resolution
* **Organized** – through VLANs for department-wise isolation
* **Redundant** – with backup default routes for failover and reliability

This setup mirrors real corporate environments and offers hands-on experience in applying industry-standard practices. It's ideal for academic use, practical learning, and showcasing enterprise networking skills in labs, demos, or internship interviews.



## 🔐 Login & Access Credentials

| Access Type            | Username | Password   |
|------------------------|----------|------------|
| Console Login          | –        | `cisco`    |
| Enable Secret          | –        | `cisco`    |
| SSH Remote Access      | `admin`  | `admin`    |
| Wireless (Per VLAN)    | –        | `sales123`, `hr123`, etc. (WPA2) |

> Standardized credentials make access and troubleshooting easier across devices.



## 🧠 Project Features

| Feature       | Purpose                             |
|---------------|-------------------------------------|
| **VLANs**     | Departmental segmentation           |
| **OSPF**      | Dynamic and scalable routing        |
| **NAT (PAT)** | Internet access for internal hosts  |
| **SSH**       | Secure remote CLI access            |
| **DHCP**      | Automatic IP address assignment     |
| **DNS**       | Domain name resolution              |
| **ACLs**      | Traffic filtering and control       |
| **Port Security** | Device-level port access        |
| **Wireless**  | VLAN-specific wireless SSIDs        |
| **Redundancy**| Weighted routes for backup ISP links|



## 🖧 IP Address Table (Sample)

| VLAN | Department | Subnet              | Gateway IP     |
|------|------------|---------------------|----------------|
| 10   | Sales      | 172.16.1.0/25       | 172.16.1.1     |
| 20   | HR         | 172.16.1.128/25     | 172.16.1.129   |
| 30   | Admin      | 172.16.2.0/25       | 172.16.2.1     |
| 40   | IT         | 172.16.2.128/25     | 172.16.2.129   |
| 50   | Finance    | 172.16.3.0/25       | 172.16.3.1     |
| 99   | BlackHole  | 192.168.99.0/24     | 192.168.99.1   |

- **DNS Server:** `172.16.3.130`
- **Default Route:** `0.0.0.0 0.0.0.0 gig1/0/2 70`



## 📶 Wireless SSIDs

| Department | SSID        | VLAN | Password  | Security |
|------------|-------------|------|-----------|----------|
| Sales      | SalesWiFi   | 10   | sales123  | WPA2     |
| HR         | HRWiFi      | 20   | hr123     | WPA2     |
| Admin      | AdminWiFi   | 30   | admin123  | WPA2     |

---

## ⚙️ Key Configuration Commands

### 🔐 Basic Security

```bash
line console 0
 password cisco
 login
enable secret cisco
service password-encryption
````

### 🖥 Hostname and Domain

```bash
hostname CORE-R1
no ip domain-lookup
ip domain-name cecos.com
```

### 🔑 SSH Access

```bash
crypto key generate rsa
username admin secret admin
line vty 0 4
 login local
 transport input ssh
```

### 🔀 VLAN Creation & Port Assignment

```bash
vlan 10
 name Sales
interface fastEthernet0/1
 switchport mode access
 switchport access vlan 10
```

### 🌐 Trunking

```bash
interface gigabitEthernet0/1
 switchport trunk encapsulation dot1q
 switchport mode trunk
```

### 🛡 Port Security

```bash
interface fastEthernet0/5
 switchport port-security
 switchport port-security maximum 1
 switchport port-security mac-address sticky
 switchport port-security violation shutdown
```

### 🧭 OSPF Routing

```bash
router ospf 1
 network 172.16.1.0 0.0.0.127 area 0
```

### 🧭 Static Default Route (Weighted)

```bash
ip route 0.0.0.0 0.0.0.0 gig1/0/2 70
```

### 🗂 DHCP Setup

```bash
ip dhcp pool SALES
 network 172.16.1.0 255.255.255.128
 default-router 172.16.1.1
 dns-server 172.16.3.130
```

### 🌍 NAT with ACL

```bash
access-list 1 permit 172.16.1.0 0.0.0.127
ip nat inside source list 1 interface Serial0/2/1 overload
```

### 🧭 DNS Server Entry

```bash
ip host www.cecos.com 172.16.3.130
```

### 📣 DHCP Relay

```bash
interface vlan 10
 ip helper-address 172.16.3.130
```


## 🔍 Verification & Troubleshooting

```bash
show ip interface brief
show vlan brief
show ip ospf neighbor
show mac-address-table
ping 8.8.8.8
```


## 📊 Conclusion

This enterprise network design is an end-to-end simulation of a real-world scalable and secure corporate setup. It incorporates advanced networking concepts like inter-VLAN routing, OSPF, NAT, DHCP-DNS integration, and wireless configuration. This project is ideal for academic demonstration, personal learning, or as a portfolio piece for internships and job applications.


## 📁 Files Included

* `.pkt` file (Packet Tracer network)
* `README.md` (This document)
* Network topology image (Optional)

