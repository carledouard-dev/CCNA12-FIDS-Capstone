# Inter Zone Routing Paths
Owner: Carl Edouard (Backbone Owner)

## Layout

```
                          Router0
                         10.0.0.33
                       /     |     \
               .0/30  /      |      \  .12/30
                     /       |       \
  ENG   --+         /        |        \         +--  DMZ
  CORP  --+--  MS0 +       .16/30      + MS1  --+
  GUEST --+  10.0.0.35       |      10.0.0.36   +--  MGMT
                     \       |       /
               .4/30  \      |      /  .8/30
                       \     |     /
                          Router1
                         10.0.0.34
```

## Border routers
Multilayer Switch0 is the border router for Engineering, Corporate and Guest (Areas 1, 2, 3).
Multilayer Switch1 is the border router for the DMZ (Area 4) and connects Management.
Router0 and Router1 sit in Area 0, the backbone.

## Router IDs
Router IDs come from Jaden's addressing plan: Router0 10.0.0.33, Router1 10.0.0.34, MS0 10.0.0.35, MS1 10.0.0.36.
Each ID is a loopback address. A loopback never goes down, so a device keeps the same ID even when we pull a cable during failover testing.

## How traffic moves between zones
Each multilayer switch connects to both routers, so there are always two ways between MS0 and MS1: through Router0 or through Router1.

Example: Corporate to DMZ goes MS0, then Router0 or Router1, then MS1.

OSPF uses both paths at the same time. If one link goes down, traffic moves to the other one on its own. We prove this in the Week 6 failover test.

## Where the rules are enforced
Engineering, Corporate and Guest all connect to MS0, so traffic between them never reaches the routers. If we only put ACLs on the routers, a Guest PC could reach Engineering without ever being checked. So the rules between those three zones go on MS0, and the DMZ rules go on MS1, right in front of the servers.

## What happens when something breaks
If one switch to router link fails, traffic takes the other router. If a whole router fails, the other one carries everything. The Router0 to Router1 link is an extra backup and doesn't affect users if it drops. The one thing this design can't survive is losing MS0 or MS1 itself, since each zone connects to only one switch. We'll note that in the final report as a future improvement.

## Links
MS0 to Router0: 10.0.255.0/30
MS0 to Router1: 10.0.255.4/30
MS1 to Router1: 10.0.255.8/30
MS1 to Router0: 10.0.255.12/30
Router0 to Router1: 10.0.255.16/30

## OSPF settings
Each ABR summarizes its zones (for example `area 1 range 10.1.0.0 255.255.252.0`), so the backbone only sees one route per zone. Backbone links use MD5 authentication so an untrusted device can't inject routes. User facing VLANs are passive so PCs never hear OSPF traffic.

## How we'll check it in Week 3
`show ip ospf neighbor` shows every neighbor FULL. `show ip route ospf` on Router0 shows only the four zone summaries. A traceroute from Corporate to the DMZ, run again with one uplink shut, shows traffic switching routers.
