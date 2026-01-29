# Security Controls

---

## Overview

This document outlines the security mechanisms implemented to protect the WAN, restrict unauthorized access, and reduce risk across the simulated enterprise environment.

The goal was to apply layered defensive controls that reflect real-world enterprise network hardening practices.

Network architecture and addressing details are documented separately in:

- Network_Design_Document.md
- IP_Addressing_Plan.md

---

## Security Objectives

The network was secured to achieve the following:

- Prevent unauthorized device access
- Limit lateral movement between departments
- Protect critical infrastructure systems
- Restrict guest network privileges
- Secure management access to network devices
- Reduce attack surface at both Layer 2 and Layer 3

---

## Layered Security Approach

Security was applied at multiple layers:

- Segmentation (VLANs)
- Traffic filtering (ACLs)
- Port-level protection (Port Security)
- Device hardening (SSH, authentication, passwords)

This defense-in-depth strategy ensures that failure of a single control does not expose the entire network.

---

## VLAN Segmentation

Logical segmentation separates departments into independent broadcast domains.

### Purpose
- Reduce attack surface
- Prevent unnecessary inter-department communication
- Contain potential compromises
- Improve traffic isolation

### Result
Devices in separate VLANs must route through the gateway, where policies can be enforced.

---

## Access Control Lists (ACLs)

ACLs were implemented to control traffic between network segments.

### Use Cases
- Restrict guest devices from accessing internal resources
- Protect sensitive servers
- Enforce least-privilege communication
- Limit unnecessary cross-network traffic

### Benefits
- Centralized traffic control
- Improved security posture
- Reduced lateral movement risk

---

## Port Security

Switch port security was enabled on access ports to prevent unauthorized devices from connecting to the network.

### Controls Applied
- Sticky MAC address learning
- Maximum MAC address limits
- Automatic violation handling

### Benefits
- Blocks rogue or unknown devices
- Prevents MAC flooding attacks
- Enhances physical network protection

---

## Device Hardening

Routers and switches were configured using secure management practices.

### Hardening Measures

- SSHv2 enabled for remote management
- Telnet disabled
- Encrypted passwords
- Local authentication required
- Console login protection
- Login banners configured
- Unused ports administratively disabled

### Benefits
- Protects management plane
- Prevents credential interception
- Reduces exposure to unauthorized access

---

## Management Security

Administrative access was restricted to authorized users only.

### Practices
- Password-protected console and VTY access
- Encrypted remote sessions (SSH)
- Limited management exposure

These controls help protect against unauthorized configuration changes.

---

## Validation and Testing

The following checks were performed to verify controls:

### VLAN isolation
- Confirm devices cannot directly communicate across VLANs without routing

### ACL enforcement
- Test blocked vs allowed traffic flows

### Port security
- Attempt unauthorized device connections
- Verify violations are triggered

### Management protection
- Confirm SSH access works
- Confirm Telnet is unavailable

Expected results:
- Only permitted traffic succeeds
- Unauthorized access attempts fail

---

## Security Best Practices Applied

- Principle of least privilege
- Network segmentation
- Defense in depth
- Secure management protocols
- Minimized attack surface
- Continuous validation

---

## Skills Demonstrated

- VLAN-based segmentation
- ACL traffic filtering
- Switch port security
- Network device hardening
- Secure remote administration
- Enterprise-style security architecture

