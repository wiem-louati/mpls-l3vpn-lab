# MPLS Layer 3 VPN Lab

**A networking lab exploring provider routing, VPN separation and connectivity across an MPLS backbone.**

## Overview

This project focused on building an MPLS Layer 3 VPN environment using Cisco routers in a virtual lab.

The objective was to understand how a service provider can transport traffic for multiple customer networks over a shared backbone while maintaining separate routing environments.

## Architecture

The topology followed a service-provider architecture:

- **Customer Edge (CE) routers:** connect customer networks to the provider.
- **Provider Edge (PE) routers:** maintain customer VRFs and exchange VPN routes.
- **Provider (P) routers:** forward labelled traffic across the backbone.

Customer routing information was separated through Virtual Routing and Forwarding instances on the PE routers.

## Technical Implementation

### Provider backbone

The provider network established IP reachability between backbone routers. MPLS and LDP were used to distribute transport labels and enable labelled forwarding across the core.

### Customer routing separation

I configured VRFs on the PE routers to create separate customer routing tables.

Route Distinguishers identified VPN routes, while Route Targets controlled their import and export between VRFs.

### VPN route exchange

I configured MP-BGP with the VPNv4 address family between PE routers to exchange customer VPN routes and their associated VPN labels.

Together, these components enabled customer traffic to traverse the shared provider backbone.

## Validation

The validation process was organised around the following checks:

| Area | Behaviour to verify |
|---|---|
| Backbone routing | Provider routers can reach the required backbone addresses |
| LDP | Neighbour relationships form and transport labels are exchanged |
| MP-BGP | VPNv4 sessions establish and expected VPN routes are received |
| VRFs | Customer routes appear in the appropriate routing tables |
| End-to-end connectivity | Sites belonging to the same VPN can communicate |
| VPN separation | Separate VPNs remain isolated unless route sharing is explicitly configured |

Packet captures and router command outputs can provide supporting evidence for these checks.

## Troubleshooting Approach

I approached troubleshooting in layers: backbone reachability, MPLS label distribution, MP-BGP route exchange, VRF route import and export, and customer connectivity.

This structure helps identify whether a connectivity problem originates in the provider transport network or in the customer VPN configuration.

## Skills Developed

- Understanding MPLS forwarding and label distribution
- Configuring customer routing separation with VRFs
- Understanding Route Distinguishers and Route Targets
- Configuring MP-BGP VPNv4 route exchange
- Investigating connectivity across several routing layers
- Distinguishing VPN traffic separation from encryption

## Key Takeaway

This project helped me understand how routing protocols, MPLS labels and VPN routing tables work together to deliver connectivity across a shared infrastructure.

It also reinforced the importance of validating both successful communication and the boundaries between separate customer networks.

## Repository Scope

This initial version provides a project overview. Configuration files, topology diagrams and validation evidence will be added as available.
