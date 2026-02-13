# NetworkingLabs

This repository contains networking labs built in GNS3.  

The goal of this project is to document practical networking implementations, and whatever else we cook up.

---

## Lab Structure

Each lab is organized by technology and contains:

- `README.md` – Lab guide and explanation
- `topology.png` – Topology diagram
- `.conf` files – Device configurations for all routers/switches in the lab

Every lab folder is self-contained so it can be recreated or ripped independently.

---

## Platforms Used

These labs are currently built using:

- **Cisco 7200 (Dynamips)** – IOS 12.4(5)T
- **Cisco vIOS L2** – Version 15.2
- Emulated and run in **GNS3**

---

## Vendor Scope

Most current labs are built on Cisco platforms.

However, I plan to expand into:

- Juniper (Junos)
- Multi-vendor routing scenarios
- Interoperability testing

I really enjoy Junos syntax and will be incorporating Juniper-based labs in future updates.

---

## Reproducing Labs

To recreate a lab:

1. Open GNS3.
2. Build the topology shown in `topology.png`.
3. Apply the provided `.conf` files to each device.
4. Verify using standard show/debug commands described in the lab guide.


