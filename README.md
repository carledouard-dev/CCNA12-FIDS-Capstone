# CCNA12 FIDS Capstone

Secure Campus Segmentation and Access Control for Fairmont Integrated Defense Solutions (FIDS).
Cisco track, IT 491 Capstone, NJIT, Fall 2026. Sponsor: FIDS. Platform: Cisco Packet Tracer 8.2 or later.

## What we are building

A campus network split into five security zones. Each zone gets its own VLAN and its own OSPF area, and extended ACLs at every zone border decide which traffic is allowed to cross. Then we prove it works: every pair of zones is tested in both directions, and ACL hit counters show the rules doing their job.

| Zone | OSPF area | Owner |
|---|---|---|
| Management backbone | Area 0 | Carl |
| Engineering | Area 1 | Jaden |
| Corporate | Area 2 | Michael |
| Contractor/Guest | Area 3 | Michael |
| Server/DMZ | Area 4 | Devam |

VLAN IDs, subnets and router IDs live in the addressing plan inside `design/`. That file is the single source of truth, so the numbers are not repeated here.

## Team

| Member | Role | GitHub |
|---|---|---|
| Carl Edouard | Project Manager and backbone owner | @carledouard-dev |
| Jaden Torres | Zone policy and addressing lead | @Eztorr |
| Michael Pietrewicz | Verification and testing lead | @mpietrewicz11 |
| Devam Patel | Security, documentation and diagram lead | @ddevammm |

## Where things go

| Folder | What lives there | Owner |
|---|---|---|
| `docs/` | Signed scope, schedule, weekly PM reports | Carl |
| `design/` | Addressing plan, zone policy matrix, router ID scheme | Jaden |
| `configs/` | Exported running config from every device, one file per device | Devam |
| `diagrams/` | Logical and physical topology diagrams | Devam |
| `testing/` | Appendix F test log and all evidence, named by test ID | Michael |
| `notes/` | One intro note per member | Everyone |

## Team rules

1. Commit the `.pkt` file and any changed configs at the end of every working session. If it is not in the repo, it did not happen.
2. Nothing gets configured until the sponsor approves the addressing plan and policy matrix.
3. Every ACL is checked line by line against the policy matrix before it goes on a device.
4. Commit messages say what changed and why, for example: `Engineering ACL: block Contractor to Eng file share (matrix row 3)`.

## Tracking

Sprints and tasks: Jira, ccna12-fids.atlassian.net. Weekly status: PULSE. Schedule: `docs/`.
