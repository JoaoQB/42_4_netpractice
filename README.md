# **42_4_NetPractice**

## **TCP/IP**

TCP/IP is a model to standardise internet connections. It is a reliable way of transfering data, or packets, between devices connected to the internet.
Here's how it works:

### **Layer Structure**

Here’s the table with the "Internet" row included for clarity:

---

|          **User**          |
|----------------------------|
| 4 - **Application Layer**  |
| 3 - **Transport Layer**    |
| 2 - **Network Layer**      |
| 1 - **Data Link Layer**    |
|        **Internet**        |

Depending on whether data is being sent or received, it goes through all four layers, each adding a `header` of information. This process is known as `encapsulation` (for sending data) or `decapsulation` (for receiving data).

1. `Application Layer`: Provides the data (like HTTP or FTP).
2. `Transport Layer`: Adds end-to-end communication details (e.g., TCP/UDP).
3. `Network Layer`: Adds IP address and routing information.
4. `Data Link Layer`: Adds local MAC addresses for physical data transfer.

When data is sent, it moves through these layers until it reaches the `physical layer`, where the actual data transmission (e.g., via cables) occurs. On receipt, it goes back through these layers to reach the user.

| **Layer Breakdown** |
|---------------------|
4 - **Application Layer** - (HTTP, FTP, SMTP)    - DATA                          - **Data**
3 - **Transport Layer**   - (TCP, UDP)           - TCP|DATA                      - **Segment**
2 - **Network Layer**     - (IP, Routers)        - IP|TCP|DATA                   - **Packet**
1 - **Data Link Layer**   - (Ethernet, Switches) - ETHERNET|IP|TCP|DATA|ETHERNET - **Frame**


## **Transport Layer** - TCP

The `Transmission Control Protocol` (TCP) ensures reliable data transfer by breaking down large amounts of information into smaller packets, sending them across the network, and reassembling them in the correct order. TCP also handles error correction and congestion control.

## **Network Layer** - IP

IP addressing assigns unique addresses to devices on a network. Each device requires a unique IP address to connect to the internet.

For this project, only IPv4 (not IPv6) is used, which defines the IP address as a 32-bit number, represented as four 8-bit blocks. An IP address has two main parts:
- `Network ID`: Identifies the network.
- `Host ID`: Identifies the device within the network.

A `subnet mask` helps separate these parts. For example, `104.95.23.12` in binary is `01101000.01011111.00010111.00001100`.

### **Public Addresses**

Public IPs are accessible directly over the internet, assigned to the network router by your ISP. They connect devices from within your network to the outside.

### **Private Addresses**

Private IPs are used within local networks, assigned by the network router to devices within that network. They allow devices within the same network to communicate. Private IPs aren’t accessible directly from the internet, ensuring security and making it easier to manage IPs internally.

**Private IP Ranges:**
- **Class A**: `10.0.0.0 - 10.255.255.255` (Subnet mask: `255.0.0.0` /8)
- **Class B**: `172.16.0.0 - 172.31.255.255` (Subnet mask: `255.240.0.0` /12)
- **Class C**: `192.168.0.0 - 192.168.255.255` (Subnet mask: `255.255.0.0` /16)

`10.0.0.0 - 10.255.255.255`

Class A private range with a subnet mask of 255.0.0.0 (/8), meaning the first 8 bits (10) define the network and the remaining 24 bits ar for hosts. This range supports a large number of IP's. (16,777,216 addresses)

`172.16.0.0 - 172.31.255.255`

Class B private range with a subnet mask of 255.240.0.0 (/12), meaning the first 12 bits (172.16 to 172.31) define the network. That is why it stops at 31 instead og extending to 255.(1,048,576 addresses)

`192.168.0.0 - 192.168.255.255`

Class C private range with a subnet mask of 255.255.0.0 (/16), meaning the first 16 bits (192.168) define the network. It stays at 192.168 as this is the boundary defined by the 16-bits mask. (65,536 addresses)

### **Loopback Addresses**

Loopback addresses (127.0.0.0 - 127.255.255.255) are reserved for internal device testing and communication. The address `127.0.0.1`, known as `localhost`, allows applications on the same device to communicate without external network access.

This setup ensures private networks avoid conflicts with public IPs and facilitates device-specific testing and communication.

## Masks (subnet mask)

A subnet mask is a 32-bits address used to distinguish between a network address and a host addres in the IP address.
It defines the range that can be used within a network or a subnet.

It is often represented as a series of numbers, typically in the form of four octets separated by perios, such as 255.255.255.0
We can represent this number in bits which would give 11111111.11111111.111111111.00000000

Let's take a device as example:

Interface A1
	IP: 104.198.241.125
	Mask: 255.255.255.128

To determine hich portion of the IP address is the network address we need to apply the mask to the IP address. We first convert the mask to it's binary form:

Mask: 11111111.11111111.11111111.10000000

### Converting a decimal number into binary

Let's say we want to convert the decimal number 16 to binary:
	1: Divide by 2: Divide the number (16) by 2. Write down the remainder. If it divides evenly the ermainder is 0, if not the remainder is 1.
	2: keep dividing: take the result (the quotient) and divide by 2 until you reach 0, each tme writing down the remainder.
	3; Read from bottom to top: The binary result is the sequence of remainders, read from bottom to top.

16:

16 / 2 = 8, remainder: 0
8 / 2 = 4, remainder: 0
4 / 2 = 2, remainder: 0
2 / 2 = 1, remainder: 0
1 / 2 = 0, ermainder: 1

So 16 in binary is: 10000.

### Converting binary to a decimal number

Let's say we want to read the binary number 11001:
	1: Identify the positions: starting from the right label each position with a power of 2.
		The rightmost position is 2^0, the next is 2^1, then 2^2, 2^3, and so on.
		For example in 11001 the positions are: 11001, 1 pos 4, 1 pos 3, 0 pos 2, 0 pos 1, 1 pos 0.
	2: Calculate the value of each 1: For each position that has a 1, calculate the value of that power of 2.
		Only positions with a 1 contribute to the total. If the position has a 0 it doesn't add anything.
	3: Add up the values.

11001:

1 pos 4, 2^4 = 16
1 pos 3, 2^3 = 8
1 pos 0, 2^0 = 1

16 + 8 + 1 = 25

11001 equals 25 in decimal number.
