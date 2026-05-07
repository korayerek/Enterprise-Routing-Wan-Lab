# Routing & WAN Lab (Multi-Site Network)

## Overview

In this project, I built a multi-site network topology to simulate real-world branch-to-HQ connectivity using Cisco Packet Tracer.

The goal was to understand how routers communicate over WAN links and how routing decisions are made using both static and dynamic routing protocols.

The topology includes three sites:
- Headquarters (HQ)
- Branch 1
- Branch 2

Each site has its own LAN and is connected through routed WAN links.

---

## Objectives

- Configure router-to-router communication across multiple sites
- Implement static routing and default routes
- Understand path selection behavior
- Configure OSPF for dynamic routing
- Control routing paths using OSPF cost
- Simulate and verify failover scenarios
- Validate connectivity using ping and traceroute

---

## Topology

- 3 routers (HQ, Branch1, Branch2)
- 3 switches (Layer 2)
- 3 LAN segments
- 3 WAN links:
  - HQ ↔ Branch1
  - HQ ↔ Branch2
  - Branch1 ↔ Branch2 (used as backup path)

---

## Phase 1: Static Routing

In the first phase, I configured static routing to establish connectivity between all sites.

- Branch routers were configured with a default route pointing to HQ
- HQ router was configured with static routes to both branch LANs

During initial testing, traffic did not pass through HQ as expected. I identified that a more specific static route between Branch 1 and Branch 2 was overriding the default route.

After removing the incorrect static route, traffic correctly flowed through HQ as intended.

This helped reinforce my understanding of route selection, especially how longest prefix match takes priority over administrative distance.

I used `ping` and `traceroute` to verify the routing behavior.

---

## Phase 2: OSPF (Dynamic Routing)

In the second phase, I replaced static routes with OSPF.

- OSPF was configured on all routers (Area 0)
- All LAN and WAN networks were advertised
- Routers dynamically learned all routes

To control path selection:
- I increased the OSPF cost on the direct Branch1–Branch2 link
- This forced traffic to prefer the HQ path under normal conditions

---

## Failover Testing

To test network resilience:

- I shut down the primary link between HQ and Branch1
- Traffic automatically rerouted through the Branch1–Branch2 link

This demonstrated OSPF convergence and failover behavior.

---

## Verification

I validated the network using:

- `show ip route` (to confirm route learning)
- `show ip ospf neighbor` (to verify adjacency)
- `ping` (to confirm connectivity)
- `traceroute` (to verify path selection and failover)

Screenshots are included to show both normal operation and failover scenarios.

---

## Screenshots

See the `/screenshots` folder for:

- Static routing route tables (Phase 1)
- OSPF neighbors and routing tables (Phase 2)
- Traceroute results (primary and failover paths)

---

## Key Takeaways

- Static routing is simple but not scalable
- OSPF enables dynamic routing and faster convergence
- Route selection depends on longest prefix match before administrative distance
- Path preference can be controlled using OSPF cost
- Failover behavior can be simulated and validated in a lab environment
- Understanding routing tables is critical for troubleshooting

---

## Tools Used

- Cisco Packet Tracer
- Cisco IOS CLI

---

## Notes

Sensitive information such as device credentials has been simplified for lab purposes.