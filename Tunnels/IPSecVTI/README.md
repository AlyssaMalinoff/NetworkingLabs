# IPSec Static Virtual Tunnel Configuration

site-to-site VPN configuraton using a statically configured tunnel. 

## Key Concepts
- Understand how a GRE tunnel forms and functions
- Understand how to configure and setup various IPSec components on a tunnel interface (`transform-set`, `ipsec profile`, `isakmp key`)
- How to apply IPSec configurations to your interfaces
- Differences in traditional GRE+IPSec implementations and using a tunnel interface (having to define traffic with access-lists and crypto-maps)