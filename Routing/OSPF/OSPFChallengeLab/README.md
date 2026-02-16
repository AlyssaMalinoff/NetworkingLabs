# OSPF Professional Lab

The original guide for this lab can be found at:
https://networklessons.com/labs/ospf-professional-lab-1

This lab implements a multi-Area OSPF topology with:
- OSPF Basic Configurations
- Security and Authentication
- Route Filtering and Summarization
-LSA and Distribute-list Fitlering
- IPv6 Migration (OSPFv3)
  

---

# Challenge Lab

Starting router configurations are included, and below is a list of requirements to implement in the lab. Router configuration files are posted for completed lab.

---
## Lab Requirements:

### IPv4 Addressing
- All routers will have a Loopback0 interface with a /32 IPv4 address corresponding to the router name. For example, R5 will have a Loopback0 configured with an address of 5.5.5.5/32.
- The Internet will be assigned the IP address of 203.0.113.2. (Simulate this using any device with the IP address and the default gateway set to the IP address of the GigabitEthernet0/0 interface of R1.)
- 192.168.5.10/24 will be used as the IP address for the host connected to R7 in Area 2, and 192.168.5.7 will be configured as its default gateway
-Networks:
    - 20.20.20.0/24 will be used for the network of routers in Area 0
    - 20.20.30.0/24 will be used for the network between R7 and R8 in the discontiguous Area 0
    - 192.168.1.0/24 will be used for the network between R4 and R5 in Area 51
    - 192.168.2.0/24 will be used for the network between R2 and R5 in Area 51
    - 192.168.3.0/24 will be used for the network of routers in Area 3
    - 192.168.5.0/24 will be used for the host network connected to R7 in Area 2
    - 192.168.6.0/24 will be used for the network between R3 and R7 in Area 2
    - 192.168.20.0/24 will be used for the network between R5 and R6
    - 203.0.113.4/30 will be used for the network between R1 and the Internet.
    - 172.16.10.6/24 will be assigned to Loopback1 of R6
    - 172.16.11.6/24 will be assigned to Loopback2 of R6
    - 172.16.12.6/24 will be assigned to Loopback3 of R6
    
### IPv6 Addressing
- You must use the 2001:db8::/32 global unicast prefix.
- Routers R1, R2, R3, R4, R5, and R7 will all have Loopback 10 configured on each, with a /64 IPv6 network assigned.
- The network interfaces of R1 and the device acting as the Internet will also be assigned a global unicast /64 IPv6 address.

### Area 0
- Enable OSPF on all Area 0 interfaces on R1, R2, R3, and R4 and verify that OSPF neighbors have been established.
- Configure all four routers to advertise their loopback addresses as well as their Area 0 connected networks via OSPF.
- Advertise a default route from R1 to all other routers in Area 0. Make sure that this default route will be advertised regardless of whether or not R1 has a configured default route.
- Configure a static default route on R1 that will direct traffic to the Internet.
- Ensure that R3 becomes the DR and R2 becomes the BDR for the 20.20.20.0/24 network segment.

### Area 2
- Enable OSPF on all Area 2 interfaces on R3 and R7, including R7’s loopback interface, and verify that OSPF neighbors have been established.
- Configure GigabitEthernet 0/2 on R7 to stop searching for potential OSPF neighbors, but to allow the connected subnet to still participate in OSPF.

### Area 51
- Enable OSPF on all Area 3 interfaces on R3, R9, and R10.
- Configure all routers to advertise their Area 3 networks, and configure R9 and R10 to advertise their loopback addresses via OSPF.
- Configure these routers to use a point-to-multipoint non-broadcast network type.
- Configure R3 to become neighbors with R9 and R10 and verify neighbor adjacencies
- Configure the hello and dead intervals on these OSPF routers to correspond to double the default values.
- Configure Area 3 as a Stub area.

### Non-COntiguous Area 0
- Enable OSPF on all Area 0 interfaces on R7 and R8 and verify that OSPF neighbors have been established.
- Configure R7 and R8 to advertise their Area 0 interfaces via OSPF.
- Configure R8 to advertise its loopback address via OSPF.
- Create a Virtual Link between R3 and R7 to ensure the non-contiguous Area 0 is correctly connected to the backbone network 

### Security and Authentication
- Configure plain text authentication between R5 and R4, as well as between R5 and R2, and ensure that the new neighbor adjacencies have come up.
- Configure a TTL security check between R5 and R4 and between R5 and R2. Apply the configuration on a per-interface basis. Make sure to configure the number of hops explicitly and as restrictively as possible.
- You decide that plain text authentication is too risky. For the R5 – R4 neighbor adjacency, change the authentication to MD5, and for the R5 – R2 adjacency, change the authentication to SHA-HMAC.

### Load Balancing and Path Preference 
- Configure OSPF such that all traffic from Area 0 destined to networks within Area 51 and beyond will be routed via R4 only. If R4 fails, only then should R2 be used. This should be achieved by manipulating the OSPF cost on particular interfaces, and examining the reference bandwidth.
- Configure OSPF within Area 51 so that all traffic destined for the Internet is routed via R2. If R2 fails, only then should such traffic be routed via R4. All traffic destined to internal networks should be load-balanced across R2 and R4. To achieve this, consider changing the type of stub that Area 51 is configured as. Do not remove the stub configuration completely. 

### LSA and Distribute-List Filtering
- Prevent the loopback addresses of all of the routers in Area 0 from being advertised within Area 3.
- Prevent any OSPF routers from learning about the 192.168.20.0/24 network. Do this by using a route map on the local router.
- Prevent R10 from installing a route to the 192.168.2.0/24 network into the routing table. The route should still be visible in the OSPF LSDB.

### Summarization
- Ensure that the networks found within Area 2 are summarized as efficiently as possible.
- Configure summarization on R5 so that the networks redistributed into OSPF within Area 51 are summarized as efficiently as possible.

### IPv6 Migration Update
- IPv6 routing must be enabled on all of the routers involved in IPv6 routing.
- Enable all of the appropriate router interfaces with IPv6 so that OSPFv3 will be able to function between the listed routers.
- The network between R1 and the device acting as the Internet will be assigned IPv6 addresses in the 2001:db8::/64 prefix. The appropriate IPv6 default gateway should also be assigned to the Internet device.
- The network between R7 and the host H1 will be assigned IPv6 addresses in the 2001:db8:0:A::/64 prefix. The appropriate IPv6 default gateway should also be assigned to the host device.
- The rest of the interfaces between routers will not be assigned global unicast addresses but will use their Link-Local addresses for OSPF operations.
- The following routers will be configured with a Loopback10 interface with a /64 global unicast IPv6 address as follows:
    - R1’s Loopback10 interface will be assigned 2001:db8:0:1::1/64
    - R2’s Loopback10 interface will be assigned 2001:db8:0:2::1/64
    - R3’s Loopback10 interface will be assigned 2001:db8:0:3::1/64
    - R4’s Loopback10 interface will be assigned 2001:db8:0:4::1/64
    - R5’s Loopback10 interface will be assigned 2001:db8:0:5::1/64
    - R7’s Loopback10 interface will be assigned 2001:db8:0:7::1/64

### OSPFv3 in Area 0, 2, and 51
- Enable OSPFv3 operation in areas 0, 2, and 51, excluding the discontiguous area 0 such that all of the above IPv6 networks assigned to the loopback interfaces are reachable to each other.

### IPv6 Default Route
- Configure an IPv6 default route to the Internet such that all IPv6 routers in the topology can reach the Internet.

### OSPFv3 Authentication and Encryption 
- Configure Authentication and Encryption for OSPFv3 between all routers in Area 0, ensuring that OSPFv3 adjacencies are maintained.


