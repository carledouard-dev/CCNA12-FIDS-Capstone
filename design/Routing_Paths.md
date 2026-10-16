# Inter Zone Routing Paths
Owner: Carl Edouard (Backbone Owner)

## Border routers
Multilayer Switch0 is the border router for Engineering, Corporate and Guest (Areas 1, 2, 3).
Multilayer Switch1 is the border router for the DMZ (Area 4) and connects Management.
Router0 and Router1 sit in Area 0, the backbone.

## Router IDs
Router IDs come from Jaden's addressing plan: Router0 10.0.0.33, Router1 10.0.0.34, MS0 10.0.0.35, MS1 10.0.0.36.

## How traffic moves between zones
Each multilayer switch connects to both routers, so there are always two ways between MS0 and MS1: through Router0 or through Router1.

Example: Corporate to DMZ goes MS0, then Router0 or Router1, then MS1.

OSPF uses both paths at the same time. If one link goes down, traffic moves to the other one on its own. We prove this in the Week 6 failover test.

## Links
MS0 to Router0: 10.0.255.0/30
MS0 to Router1: 10.0.255.4/30
MS1 to Router1: 10.0.255.8/30
MS1 to Router0: 10.0.255.12/30
Router0 to Router1: 10.0.255.16/30
