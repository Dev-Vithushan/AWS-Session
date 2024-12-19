### **IP Address and CIDR Notation**

---

## **IP Address**
An **IP address** (Internet Protocol address) is a numerical label assigned to each device connected to a network. It serves two main purposes:
1. **Identifying the device** on the network.
2. **Locating the device** (helps with routing).

There are two types of IP addresses:
1. **IPv4** → 32-bit address (e.g., `192.168.1.1`).  
2. **IPv6** → 128-bit address (e.g., `2001:0db8:85a3:0000:0000:8a2e:0370:7334`).

---

## **CIDR (Classless Inter-Domain Routing)**
**CIDR** is a method for allocating IP addresses and routing IP traffic efficiently. It uses **prefix notation** to specify both the network and host portions of an IP address.

CIDR combines:
- An **IP address** (base address).
- A **subnet mask** (number of bits used for the network portion).

### **CIDR Notation**
The CIDR notation is written as:
```
<IP address>/<number of network bits>
```
- Example: `192.168.1.0/24`
   - **IP Address**: `192.168.1.0`
   - **/24**: The first 24 bits represent the **network**. The remaining 8 bits are for **hosts**.

---

## **Understanding CIDR Notation**
The `/n` value determines:
1. The **network portion** (fixed bits).
2. The **host portion** (variable bits used to assign IP addresses to devices).

| **CIDR**      | **Subnet Mask**     | **Number of Hosts** | **Network Size**          |
|---------------|---------------------|---------------------|---------------------------|
| `10.0.0.0/8`  | 255.0.0.0           | ~16 million         | Very large network        |
| `172.16.0.0/12` | 255.240.0.0       | ~1 million          | Large network             |
| `192.168.0.0/16` | 255.255.0.0      | ~65,000             | Medium-sized network      |
| `192.168.1.0/24` | 255.255.255.0    | 256 (254 usable)    | Small network             |
| `192.168.1.0/30` | 255.255.255.252  | 4 (2 usable)        | Very small (point-to-point link) |

---

## **How CIDR Works**
Let’s take the example `192.168.1.0/24`:
- IP Address: `192.168.1.0`.
- `/24` means **24 bits** for the network, and **8 bits** for the host.

### **Calculating Hosts**  
The number of usable hosts can be calculated as:  
```
2^(Number of Host Bits) - 2
```
- **Number of Host Bits** = 32 - 24 = 8.  
- Hosts = `2^8 - 2 = 256 - 2 = 254`.  

   **Why subtract 2?**
   - 1 IP for the **Network Address** (e.g., `192.168.1.0`).  
   - 1 IP for the **Broadcast Address** (e.g., `192.168.1.255`).

---

## **Example Breakdown**

| **CIDR**          | **Network Address** | **Broadcast Address** | **Usable IPs**        |
|--------------------|---------------------|-----------------------|-----------------------|
| `192.168.1.0/24`  | 192.168.1.0         | 192.168.1.255         | 254 usable addresses  |
| `192.168.1.0/25`  | 192.168.1.0         | 192.168.1.127         | 126 usable addresses  |
| `192.168.1.128/25`| 192.168.1.128       | 192.168.1.255         | 126 usable addresses  |

---

## **Practical Use in AWS**
When creating a VPC or subnets:
1. **Choose a CIDR block** → `10.0.0.0/16` (Large enough for 65,536 IPs).
2. **Split into subnets** → `10.0.1.0/24`, `10.0.2.0/24` for different AZs.

Example:
- VPC CIDR: `10.0.0.0/16`.  
   - Subnet A (AZ 1): `10.0.1.0/24`.  
   - Subnet B (AZ 2): `10.0.2.0/24`.  

---

### **Key Takeaways**
1. **IP Address**: The address identifying a device on the network.
2. **CIDR**: A compact way to represent IP ranges and subnetting.
3. **/n**: Specifies how many bits are reserved for the network.

