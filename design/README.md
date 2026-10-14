# Design
Owner: Jaden Torres (Zone Policy and Addressing Lead)

The plan we follow before touching any device. The sponsor approves it first.

1. Addressing plan (VLSM): every subnet and VLAN, sized so each zone shows up as one route at its border
2. VLAN to OSPF area map, with a reason for each zone
3. Router IDs and the paths traffic takes between zones (Carl)
4. Policy matrix: for every pair of zones, allow or block, and why

Once approved, these files are locked. Any change gets its own commit saying why.
