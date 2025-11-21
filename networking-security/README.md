# Networking & Security Interview Questions

## **Beginner-Level (1-20) Questions**  

### **1. What is a network?**  

A network is a group of interconnected devices that communicate to share resources and information. It can be wired or wireless.  

### **2. What is an IP address?**  

An IP (Internet Protocol) address is a unique numerical identifier assigned to each device on a network to facilitate communication.  

### **3. What is the difference between IPv4 and IPv6?**  

- **IPv4**: 32-bit addressing, supports 4.3 billion addresses.  
- **IPv6**: 128-bit addressing, supports an enormous number of addresses, improving scalability and security.  

### **4. What are private and public IP addresses?**  

- **Private IPs**: Used within local networks (e.g., 192.168.x.x).  
- **Public IPs**: Used on the internet and assigned by ISPs.  

### **5. What is a subnet mask?**  

A subnet mask divides an IP address into network and host portions, determining which part identifies the network and which part identifies the device.  

### **6. What is DHCP, and how does it work?**  

The **Dynamic Host Configuration Protocol (DHCP)** automatically assigns IP addresses to devices in a network, reducing manual configuration.  

### **7. What is DNS, and why is it important?**  

The **Domain Name System (DNS)** translates domain names (e.g., google.com) into IP addresses, making it easier to access websites.  

### **8. What is NAT (Network Address Translation)?**  

NAT allows multiple devices on a local network to share a single public IP address for internet access.  

### **9. What is a firewall?**  

A firewall is a security system that monitors and controls incoming and outgoing network traffic based on security rules.  

### **10. What are the types of firewalls?**  

- **Packet Filtering Firewall**  
- **Stateful Inspection Firewall**  
- **Proxy Firewall**  
- **Next-Generation Firewall (NGFW)**  

### **11. What is a VPN?**  

A **Virtual Private Network (VPN)** encrypts internet connections, providing secure remote access and anonymity.  

### **12. What is SSH, and why is it used?**  

SSH (**Secure Shell**) is a protocol used for secure remote access to servers using encrypted communication.  

### **13. What is HTTP and HTTPS?**  

- **HTTP (Hypertext Transfer Protocol)**: Unencrypted web communication.  
- **HTTPS (HTTP Secure)**: Secure, encrypted communication using SSL/TLS.  

### **14. What is an SSL/TLS certificate?**  

An SSL/TLS certificate encrypts website traffic, ensuring secure communication and trustworthiness.  

### **15. What is a load balancer?**  

A load balancer distributes incoming network traffic across multiple servers to optimize performance and availability.  

### **16. What are different types of load balancers?**  

- **Layer 4 Load Balancer** (Transport Layer)  
- **Layer 7 Load Balancer** (Application Layer)  

### **17. What is a DMZ in networking?**  

A **Demilitarized Zone (DMZ)** is a security buffer between an internal network and the internet, hosting public-facing services securely.  

### **18. What is port forwarding?**  

Port forwarding redirects network traffic from one port to another, often used to expose internal services externally.  

### **19. What is ARP (Address Resolution Protocol)?**  

ARP translates IP addresses into MAC addresses to enable communication within a local network.  

### **20. What is an IDS and IPS?**  

- **IDS (Intrusion Detection System)**: Monitors network traffic for threats.  
- **IPS (Intrusion Prevention System)**: Blocks malicious traffic automatically.  

---

## **Intermediate-Level (21-40) Questions**  

### **21. What is Zero Trust Security?**  

Zero Trust is a security model that assumes no entity (inside or outside the network) is trusted by default.  

### **22. What is the difference between symmetric and asymmetric encryption?**  

- **Symmetric Encryption**: Uses one key for encryption and decryption.  
- **Asymmetric Encryption**: Uses a public-private key pair (e.g., RSA).  

### **23. What is a CDN (Content Delivery Network)?**  

A **CDN** improves website speed and security by distributing content across multiple servers worldwide.  

### **24. What is the difference between TCP and UDP?**  

- **TCP**: Reliable, connection-oriented, ensures data delivery.  
- **UDP**: Faster, connectionless, best for real-time applications.  

### **25. How does a reverse proxy improve security?**  

A reverse proxy sits between users and backend servers, protecting them from direct exposure and filtering malicious traffic.  

### **26. What are the benefits of HTTPS over HTTP?**  

- Encryption  
- Data integrity  
- Authentication  

### **27. How does multi-factor authentication (MFA) enhance security?**  

MFA adds an extra security layer by requiring multiple verification methods (e.g., password + OTP).  

### **28. What is a bastion host?**  

A **bastion host** is a highly secured jump server used to access internal networks securely.  

### **29. What is OSI Model and its layers?**  

The OSI model has **7 layers**: Physical, Data Link, Network, Transport, Session, Presentation, Application.  

### **30. What is a WAF (Web Application Firewall)?**  

A **WAF** protects web applications by filtering and blocking malicious HTTP traffic.  

### **31. What is a honeypot in cybersecurity?**  

A honeypot is a security system designed to detect and study cyberattacks by mimicking real systems.  

### **32. What is BGP (Border Gateway Protocol)?**  

BGP is a routing protocol used for exchanging routing information between networks on the internet.  

### **33. What is DDoS, and how can it be mitigated?**  

A **Distributed Denial-of-Service (DDoS)** attack overwhelms a system. It can be mitigated using rate limiting, firewalls, and cloud-based protection.  

### **34. What is the CIA Triad in security?**  

The **CIA Triad** stands for **Confidentiality, Integrity, and Availability**, which are fundamental security principles.  

### **35. What is SSO (Single Sign-On)?**  

SSO allows users to log in to multiple applications using a single authentication process.  

### **36. What is a security token?**  

A **security token** is a physical or digital device used for authentication.  

### **37. What is an access control list (ACL)?**  

An ACL defines rules that allow or deny traffic based on IP, ports, or protocols.  

### **38. What is a container network security concern?**  

Containers share OS kernels, so misconfigurations can expose services to security threats.  

### **39. What is network segmentation?**  

It is dividing a network into smaller parts to improve security and performance.  

### **40. What is the difference between active and passive reconnaissance?**  

- **Active reconnaissance**: Direct interaction with the target.  
- **Passive reconnaissance**: Collecting data without direct interaction.  

---

## **Advanced-Level (41-60) Questions**  

### **41. What is mutual TLS (mTLS), and why is it used?**  

Mutual TLS (mTLS) ensures **both client and server** authenticate each other before communication, enhancing security in microservices and API interactions.  

### **42. What is the difference between L3, L4, and L7 firewalls?**  

- **L3 Firewall (Network Layer)**: Filters traffic based on IP addresses.  
- **L4 Firewall (Transport Layer)**: Filters based on ports and TCP/UDP protocols.  
- **L7 Firewall (Application Layer)**: Filters based on application-specific data (e.g., HTTP, FTP).  

### **43. How does AWS Security Groups differ from Network ACLs?**  

- **Security Groups**: Act as virtual firewalls at the instance level, stateful.  
- **Network ACLs**: Act at the subnet level, stateless.  

### **44. What is a SIEM (Security Information and Event Management) system?**  

SIEM aggregates security data from multiple sources to detect, analyze, and respond to threats.  

### **45. What is a threat model in security?**  

Threat modeling identifies potential threats and vulnerabilities in a system to proactively mitigate risks.  

### **46. What is an ephemeral port, and how is it used?**  

Ephemeral ports (e.g., **49152-65535**) are temporary ports used by client applications for outbound connections.  

### **47. How does DNSSEC enhance DNS security?**  

DNSSEC (DNS Security Extensions) prevents DNS spoofing by adding cryptographic signatures to DNS records.  

### **48. What are the different types of VPNs?**  

- **Remote Access VPN** (for individuals connecting to a network remotely).  
- **Site-to-Site VPN** (connects entire networks).  

### **49. How does a service mesh improve security in Kubernetes?**  

A **service mesh** (e.g., Istio, Linkerd) provides **mTLS, authentication, and observability** for secure communication between microservices.  

### **50. What are some common OWASP Top 10 security risks?**  

1. Injection (e.g., SQL injection)  
2. Broken Authentication  
3. Sensitive Data Exposure  
4. XML External Entities (XXE)  
5. Broken Access Control  
6. Security Misconfiguration  
7. Cross-Site Scripting (XSS)  
8. Insecure Deserialization  
9. Using Components with Known Vulnerabilities  
10. Insufficient Logging & Monitoring  

### **51. How do WebSockets handle security concerns?**  

WebSockets require **authentication, encryption (WSS), and proper origin checks** to prevent attacks.  

### **52. What is an SSRF (Server-Side Request Forgery) attack?**  

An SSRF attack tricks a server into making requests to internal services, leading to data leaks or system compromise.  

### **53. How does an AWS WAF protect applications?**  

AWS WAF filters web traffic based on **rules, rate limiting, and bot mitigation** to prevent common attacks like SQL injection and XSS.  

### **54. How does Kubernetes RBAC (Role-Based Access Control) work?**  

Kubernetes RBAC grants permissions based on **Roles, RoleBindings, ClusterRoles, and ClusterRoleBindings**, restricting access to resources.  

### **55. What is a MAC address, and how does MAC filtering enhance security?**  

A MAC address is a **unique identifier** for network interfaces. MAC filtering allows or denies network access based on these addresses.  

### **56. How does DNS poisoning work, and how can it be prevented?**  

DNS poisoning tricks users into visiting **malicious sites** by altering DNS records. Prevention includes **DNSSEC, monitoring, and secure DNS resolvers**.  

### **57. What is a federated identity in security?**  

Federated identity allows users to authenticate across multiple applications using a **single set of credentials** (e.g., Google or Microsoft sign-in).  

### **58. How does Kubernetes Network Policy improve security?**  

Kubernetes Network Policies define **rules for pod communication**, restricting traffic based on namespaces, labels, and IP ranges.  

### **59. What is the principle of least privilege (PoLP)?**  

PoLP ensures **users and applications only have the minimum access** needed to perform their tasks, reducing security risks.  

### **60. How do HSTS (HTTP Strict Transport Security) and CSP (Content Security Policy) improve web security?**  

- **HSTS**: Forces HTTPS connections to prevent downgrade attacks.  
- **CSP**: Restricts allowed content sources to prevent XSS attacks.  

---

## **📢 Contribute & Stay Updated**  

💡 **Want to contribute?**  
We **welcome contributions!** If you have insights, new tools, or improvements, feel free to submit a **pull request**.  

📌 **How to Contribute?**

- Read the **[CONTRIBUTING.md](https://github.com/abhilash/DevOps-Interview-Questions/blob/master/CONTRIBUTING.md)** guide.  
- Fix errors, add missing topics, or suggest improvements.  
- Submit a **pull request** with your updates.  

📢 **Stay Updated:**  
⭐ **Star the repository** to get notified about new updates and additions.  
💬 **Join discussions** in **[GitHub Issues](https://github.com/abhilash/DevOps-Interview-Questions/issues)** to suggest improvements.  

---

## **🌍 Community & Support**  

🔗 **GitHub:** [@abhilash](https://github.com/abhilash)  
📝 **Blog:** [ProDevOpsGuy](https://blog.prodevopsguy.xyz)  
💬 **Telegram Community:** [Join Here](https://t.me/prodevopsguy)  

