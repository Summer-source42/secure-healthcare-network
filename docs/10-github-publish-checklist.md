# GitHub Publish Checklist

Use this checklist before making the repository public.

## Must Add

- [ ] Packet Tracer `.pkt` file, if you are comfortable publishing it
- [ ] Full topology screenshot: `assets/topology/packet-tracer-full-topology.png`
- [ ] VLAN verification output: `evidence/command-outputs/show-vlan-brief.txt`
- [ ] Trunk verification output: `evidence/command-outputs/show-interfaces-trunk.txt`
- [ ] EtherChannel verification output: `evidence/command-outputs/show-etherchannel-summary.txt`
- [ ] HSRP verification output: `evidence/command-outputs/show-standby-brief.txt`
- [ ] OSPF verification output: `evidence/command-outputs/show-ip-ospf-neighbor.txt`
- [ ] Routing verification output: `evidence/command-outputs/show-ip-route.txt`
- [ ] ASA ACL/NAT verification outputs
- [ ] Connectivity test results updated in `evidence/test-results/connectivity-test-matrix.md`

## Strongly Recommended

- [ ] Add 5–8 screenshots, not 20+ random screenshots
- [ ] Crop screenshots so device names, commands, and successful results are readable
- [ ] Remove any tutorial/video wording from commit messages and documentation
- [ ] Make sure the README says “case study” or “simulated enterprise implementation,” not “YouTube project”
- [ ] Keep the tone honest: do not claim it was deployed for a real client
- [ ] Add this repo link to your resume under “Projects” or “Portfolio Case Studies”

## Suggested GitHub Description

Secure healthcare enterprise network case study with VLAN segmentation, OSPF, HSRP, EtherChannel, ASA firewall zoning, DMZ services, WLC wireless, VoIP, and verification evidence.
