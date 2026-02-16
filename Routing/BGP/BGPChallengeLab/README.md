# BGP Professional Lab

The original guide for this lab can be found at:
https://networklessons.com/labs/bgp-professional-lab-1

This lab implements a multi-AS BGP topology with:
- iBGP and eBGP peerings
- OSPF as the IGP
- BGP confederations
- IPv4 and IPv6 peerings
- Advanced BGP policy manipulation
- Route filtering and optimization
  

---

# Challenge Lab

Starting router configurations are included, and below is a list of requirements to implement in the lab. Router configuration files are posted for completed lab.

---
## Lab Requirements:

### OSPF
- Configure OSPF in ASes 23 and 4567 to prepare for the iBGP peerings.

### Tunnel
- Configure a tunnel solution so that R5 and R9 can establish a neighbor adjacency using their loopback interfaces. You are not allowed to make any changes to R8. You are allowed to create two static routes on R5 and R9.
### iBGP and eBGP IPv4 Peerings
- Configure iBGP peerings with loopback interfaces. Do not use physical interfaces.
- Configure eBGP peerings with physical interfaces, with one exception.

### eBGP IPv6 Peering
- Configure a second eBGP peering between the ISP and R1 router using IPv6. Use the IPv6 addresses on the physical interface.
- Advertise the IPv6 networks on the ISP router in BGP.

### Advertise Routes
- Advertise the directly connected IPv4 networks on the ISP router using redistribution.
- Advertise the IPv4 network of Loopback 0 on the ISP router into BGP using the network command
- Advertise the IPv6 prefixes on loopbacks 0 to 19 on the ISP router into BGP via the IPv6 peering using the network command.
- Configure AS23 to receive IPv6 routes over the IPv4 eBGP peerings with R1.
- Configure the network so that IPv6 routes are propagated into AS 1 and AS 23 but not beyond.
- Advertise the IPv4 address on the loopback interfaces of all BGP routers into BGP using the network command.

### Next-Hop Self
- Configure next hop self for IPv4 BGP peerings on all routers that require this so that traffic can be routed outside of the local AS.

### BGP Auto Summary
-Configure auto-summary on R9 to make BGP routing more efficient in the future.

### BGP Summarization
- Summarize the networks on loopback 10,11 and 12 using the most specific summary address. Ensure that only the summary network is added to the BGP table. Other networks that fall within the range of the summary have to be suppressed.

### Weight
- Configure the weight attribute of the route with a route map configuration on R4.

### Local Preference
- Configure BGP so that packets destined for network 23.45.0.0/16 from within AS 23 always exit AS 23 via router R2. Ensure no other networks are influenced.

### Path Prepending
- Configure AS path prepending on R4 and make the path via AS 4567 three times as long as the path via AS 23. Ensure no other networks are influenced.

### Origin Code
- Configure the ISP router so that other routers see network 66.77.0.0/17 with an origin code similar to a network that is not injected with redistribution. Ensure no other networks are influenced.

### MED
- Configure MED on R3 so that the path via R2 is preferred over the path via R3. Ensure no other networks are influenced.

### Prefering eBGP over iBGP
- Determine which of those possible BGP paths has been chosen as the best path and verify the reason for this using the appropriate verification commands.

### BGP Communities
- Prevent the 102.64.0.0/18 network from being advertised further downstream by R2, R3, and R4. This configuration has to be applied to R1.
- Ensure that the 123.45.0.0/17 network is advertised from R1 to ASes 23 and 4567 so that the eBGP peers will not readvertise this route to other eBGP peers.
- Ensure that the 130.25.0.0/18 network is advertised into sub-AS 45 but not into sub-AS 67 or beyond.

### Route Filtering 
- Filter out all networks with a /18 prefix length. These routes should not appear in the BGP table of R9. All configurations should be applied using prefix lists configured on R5.
- Filter out any routes with a prefix length ranging between /22 and /32. These routes should not appear in the BGP table of R9. All configurations should be applied using BGP extended access list filtering prefix lists configured on R9.

### Transit AS
- Use distribute list filtering with an access list to achieve this.

### AS Path Filtering
- Ensure that any routes that pass through AS 23 are filtered and thus are prevented from entering the BGP table of R6 using AS path filtering.
- Configure AS path filtering on R3 to remove any routers that have passed through AS 4567 but keep any routes that have originated from AS 4567.

### Route Dampening
- Enable route dampening on R2 for the networks on loopback 13, 14, and 15 of the ISP route. Use the following parameters:
	- half-life: 15
	- reuse: 750
	- suppress: 2000
	- max-suppress-time: 60

### Peer Groups
- Configure peer groups on R1 and group as many of R1’s neighbors into peer groups as possible.

### Multipath
- Configure BGP multipath so that both paths (via R2 and R3) from R1 will be chosen as the best path. No more than two paths should be chosen as the best paths. Any other paths found in the BGP table of R1 that appear multiple times and have the same Weight, Local Preference, AS Path, Origin code, MED and IGP metric should also be routed redundantly using BGP.

### Next-Hop Tracking
- Configure BGP next hop tracking on R2 so that the next hop IP addresses of R2 and R3 are actively tracked.
- Modify the next hop trigger delay to 10 seconds for the IPv4 address family.

