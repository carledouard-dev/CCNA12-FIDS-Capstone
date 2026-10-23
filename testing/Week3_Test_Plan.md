# Week 3 Test Plan

This week I'm checking that every zone can reach itself and that OSPF is up. No security rules are on yet. IPs are from the addressing plan in `design/`.

## T-01: Ping inside each zone

From each PC's command prompt.

- Engineering: PC0 pings PC1 (10.1.0.2) and the gateway (10.1.0.254)
- Corporate: PC2 pings PC3 (10.2.0.2) and the gateway (10.2.1.254)
- Guest: PC4 pings PC5 (10.3.0.2) and the gateway (10.3.0.126)
- DMZ: PC6 pings PC7 (10.4.0.2), Server1 (10.4.0.3), Server0 (10.4.0.4) and the gateway (10.4.0.14)
- Management: PC8 pings PC9 (10.0.0.19), the gateway (10.0.0.17), SW-DMZ (10.0.0.20) and SW-MGMT (10.0.0.21)

Screenshots: `T-01_ENG.png`, `T-01_CORP.png`, `T-01_GUEST.png`, `T-01_DMZ.png`, `T-01_MGMT.png`

## T-02: OSPF neighbors

`show ip ospf neighbor` on each one. Everything should say FULL.

- Router0 should see MS0, MS1 and Router1
- Router1 should see MS0, MS1 and Router0
- MS0 should see Router0 and Router1
- MS1 should see Router0 and Router1

Screenshots: `T-02_Router0.png`, `T-02_Router1.png`, `T-02_MS0.png`, `T-02_MS1.png`

Results go in the test log. If something fails I'll let the zone owner know and test it again after it's fixed.
