# DNS Lab: A Record, Local Cache, and CNAME Testing in Active Directory

## Overview

This lab demonstrates the behavior of DNS records in a domain environment, including A records, DNS caching, and the use of CNAME records. Testing was done using Azure-hosted virtual machines configured as a domain controller (DC-1) and a domain-joined client (Client-1).

## Technologies Used

- Microsoft Azure (VM deployment)
- Windows Server (Domain Controller)
- Active Directory DNS
- DNS Records (A-Record, CNAME)
- DNS Client Tools (nslookup, ipconfig)
- DNS Cache Management
---

## 1. A Record Creation and Testing

Logged into:

- **DC-1** as `mydomain.com\jane_admin`
- **Client-1** as `mydomain\jane_admin`

On **Client-1**:

- Attempted to ping `mainframe` → Request failed
- Ran `nslookup mainframe` → No DNS record found

On **DC-1**:

- Created a **DNS A Record** for `mainframe`
- Pointed the A record to **DC-1's Private IP Address**

Back on **Client-1**:

- Pinging `mainframe` now succeeded, confirming that the DNS record propagated correctly

---

## 2. DNS Cache Behavior

On **DC-1**:

- Modified the existing A record for `mainframe`, changing the IP address to `8.8.8.8`

Back on **Client-1**:

- Pinged `mainframe` again → Still resolved to the old IP address
- Ran `ipconfig /displaydns` → Confirmed the outdated address was cached locally

To refresh:

- Executed `ipconfig /flushdns` to clear the local DNS cache
- Verified cache clearance with `ipconfig /displaydns`
- Pinged `mainframe` again → Now resolved to the updated address (`8.8.8.8`)

---

## 3. CNAME Record Creation and Testing

On **DC-1**:

- Created a **CNAME Record**: aliased `search` to `www.google.com`

On **Client-1**:

- Pinging `search` resolved to Google's public address, showing successful aliasing
- Ran `nslookup search` → Confirmed that the CNAME record correctly redirected to `www.google.com`

---

## Footnote: Skills and Experience Gained

This lab provides foundational hands-on experience in Active Directory-integrated DNS management, a critical skill for system and network administrators. Key competencies developed include:

- Creating and troubleshooting **A Records** for internal name resolution  
- Observing and managing **DNS client-side caching** behavior  
- Configuring **CNAME (alias) records** for flexible DNS mappings  
- Using tools like `ping`, `nslookup`, and `ipconfig` to validate DNS functionality and diagnose issues  
- Understanding the propagation and caching process of DNS records in enterprise environments  

These skills are essential for managing scalable, secure networks and play a key role in IT operations, cybersecurity, and cloud administration.
