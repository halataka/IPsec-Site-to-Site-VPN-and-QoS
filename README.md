# IPsec-Site-to-Site-VPN-and-QoS (Cisco)

## Objective

The objective of this project was to design and implement a secure communication infrastructure that connects two networks over the internet using an IPsec Site-to-Site VPN. Additionally, Quality of Service (QoS) was applied to prioritize critical traffic and enhance overall network performance.  

This project provided hands-on experience with secure network configurations, VPN technologies, and traffic management, critical for ensuring data protection and reliability in cybersecurity. 

### Skills Learned
- Secure network design
- VLAN implementation
- IPsec VPN configuration
- QoS policy creation
- Dynamic routing using OSPF

### Tools Used
- Cisco Packet Tracer
- IPsec VPN
- OSPF
- QoS

## Project Outcome 

This project successfully secured network communication between two sites using an IPsec Site-to-Site VPN while implementing QoS policies to optimize performance. The integration of VLANs, OSPF, and encryption techniques ensured network efficiency, security, and reliability.

## Steps
### Phase One: Network Design and Configuration 
![Screenshot 2025-02-20 150105](https://github.com/user-attachments/assets/2cb91410-6dc2-49b5-819c-f1eba4bc7e86)
 *Network Topology*
#### IP Addressing Scheme 

![Screenshot 2025-02-20 150719](https://github.com/user-attachments/assets/351a793a-bd69-45dc-8f7b-e1180f8fd35f)
*IP Addressing Plan*

By logically segmenting the traffic using VLANs and subnets, network congestion was minimized, and security was enhanced by isolating different types of traffic.

#### Configuring Routers 1 and 3
Router interfaces were configured with appropriate IP addresses and subnets to ensure encrypted traffic routing. The following commands were used in privileged EXEC mode:
- interface [interface_name]
- ip address [ip_address] [subnet_mask]
- no shutdown
- show ip interface brief  # Verifies configurations

![Screenshot 2025-02-20 151158](https://github.com/user-attachments/assets/8f967949-f9de-4a30-ac47-d2a9244ba8cc)
*Router 1 IP interface brief*

![Screenshot 2025-02-20 151243](https://github.com/user-attachments/assets/232794f3-92eb-4aec-a27c-208dc6f61a21)
*Router 3 IP interface brief*

#### Switch VLAN Configuration 
VLANs were configured to segment network traffic and enhance security by isolating different types of traffic:

![Screenshot 2025-02-20 151501](https://github.com/user-attachments/assets/7a7bd79a-cc36-43cd-8855-bf0512281787)
*Switch 1 VLAN configuration*
Trunk ports were configured to facilitate VLAN-tagged traffic transfer and prepare for future VPN implementation.

#### Configuring OSPF
OSPF was implemented for dynamic routing and scalability:
![Screenshot 2025-02-20 151806](https://github.com/user-attachments/assets/68cc913d-e7ea-4534-8a40-2122183b581f)
*Router 1 OSPF*

![Screenshot 2025-02-20 151853](https://github.com/user-attachments/assets/34173bdd-3686-4833-be55-4fd85377bfea)
*Router 3 OSPF*
OSPF optimized encrypted traffic paths and aligned with QoS objectives to enhance priority services.

#### Configuring DHCP Pools
Dynamic DHCP pools were configured to manage IP addresses efficiently:
- ip dhcp pool [pool_name]
- network [subnet] [subnet_mask]
- default-router [gateway_IP]
- show ip dhcp pool mypool  # Verify configurations
![Screenshot 2025-02-20 152136](https://github.com/user-attachments/assets/750c5928-fd93-43c7-a30d-1b459396bf40)
*DHCP pools configured on Router 1*
![Screenshot 2025-02-20 152212](https://github.com/user-attachments/assets/7d1f9ed0-7bc2-4618-9116-5433912172a9)
*DHCP pools configured on Router 3*

Successful pings confirmed proper network connectivity.
![Screenshot 2025-02-20 152347](https://github.com/user-attachments/assets/56b4a1e7-7189-432c-bb66-c3bcbccc8673)
*Successful ping between PC1 and PC4*

### Phase Two: Implementing IPsec Site-to-Site VPN

#### Creating Access Lists 
Access lists were configured to define encrypted traffic flows:
![Screenshot 2025-02-20 152728](https://github.com/user-attachments/assets/00a80382-31fd-4d74-9f0d-37718ee33575)
*Router 1 ACL*

![Screenshot 2025-02-20 152728](https://github.com/user-attachments/assets/c566bd88-1a54-48c3-bcd6-ad4321bc3886)
*Router 3 ACL*

#### ISAKMP and Crypto Map Configuration 
A VPN connection was established using ISAKMP policies and a shared cryptographic key:

![Screenshot 2025-02-20 153113](https://github.com/user-attachments/assets/b72909d8-e66e-47d6-80fa-f2744d8cee49)
*Router 1 Crypto ISAKMP Protocol*

![Screenshot 2025-02-20 153200](https://github.com/user-attachments/assets/e116d480-08f5-42e3-8b00-bebb151822a1)
*Router 3 Crypto ISAKMP Protocol*

#### Defining Transform Set and Crypto Map
A transform set was defined for IPsec encryption:

![Screenshot 2025-02-20 153653](https://github.com/user-attachments/assets/e505e5e9-765d-412c-8e3e-c4e2969272bf)
*Router 1 Transform Set and Crypto Map*

![Screenshot 2025-02-20 153823](https://github.com/user-attachments/assets/22ec9b1d-9d03-499e-8a5f-b8349dca981d)
*Router 3 Transform Set and Crypto Map*

The crypto map bound the encryption settings to the outgoing interfaces:

![Screenshot 2025-02-20 153940](https://github.com/user-attachments/assets/b1554fa1-e229-4ded-93c9-a9616a80065f)
*Router 1*

![Screenshot 2025-02-20 154134](https://github.com/user-attachments/assets/00f75723-b455-4b13-9d08-cd523b091a83)
*Router 3*

Verified using show crypto ipsec sa

![Screenshot 2025-02-20 154327](https://github.com/user-attachments/assets/a9b0cee1-cd8a-419c-8f1a-4550ed18dd8a)
*Router 3 show crypto ipsec sa*

Successful pings between PC3 and PC2 validated the secure VPN tunnel.
![Screenshot 2025-02-20 154442](https://github.com/user-attachments/assets/9684fed4-5a3a-4a6e-9cca-f184a6e3d7a7)
*Updated show crypto ipsec sa on Router 3*

### Phase Three: Adding QoS
QoS policies were implemented to prioritize critical traffic:

![Screenshot 2025-02-20 154729](https://github.com/user-attachments/assets/06bdd8fc-14e4-447a-88c0-7b4bcdfb4a75)
*Router 1 QoS Policy*

Applying QoS ensured encrypted VPN packets and critical services received optimal bandwidth for high reliability.

## Key Takeaways
- Securing traffic between remote sites via IPsec VPN
- Optimizing routing efficiency with OSPF
- Prioritizing network traffic using QoS
- Enhancing security through VLAN segmentation

This project provided a real-world hands-on experience in network security, preparing for advanced cybersecurity and network administration roles.

## Future Improvements
- Implementing Multi-Factor Authentication (MFA) for enhanced VPN security
- Testing with real hardware instead of simulators
- Integrating IPv6 support for modern network infrastructure
- Expanding QoS to include VoIP and video conferencing




