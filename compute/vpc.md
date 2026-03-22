# VPC, Virtual Private Cloud

> Your own isolated network inside AWS. Every resource lives inside a VPC.

---

## 🧠 What it is
A VPC is a logically isolated section of the AWS cloud where you launch resources. You control the IP address range, subnets, route tables, internet gateways, and security settings.

---

## 🔑 Key concepts

| Concept | Description |
|---|---|
| VPC | Isolated virtual network, you define the IP range (CIDR) |
| Subnet | A subdivision of the VPC in a specific Availability Zone |
| Route Table | Rules that determine where network traffic is directed |
| Internet Gateway (IGW) | Allows communication between VPC and the internet |
| NAT Gateway | Allows private subnets to reach the internet (outbound only) |
| Security Group | Stateful firewall at the instance level |
| NACL | Stateless firewall at the subnet level |
| VPC Peering | Direct connection between two VPCs |
| VPC Endpoint | Private connection to AWS services without internet |
| Flow Logs | Captures IP traffic going in/out of network interfaces |

---

## 🏗️ Subnet types

| Type | Internet access | Use case |
|---|---|---|
| Public subnet | Yes (via IGW) | Web servers, load balancers, bastion hosts |
| Private subnet | No direct, outbound via NAT | App servers, databases, Lambda |
| Isolated subnet | None | Highly sensitive data, internal services only |

---

## 🌐 CIDR — IP address ranges

```
VPC:             10.0.0.0/16   →  65,536 IPs
  Public subnet: 10.0.1.0/24  →  256 IPs (AZ-a)
  Public subnet: 10.0.2.0/24  →  256 IPs (AZ-b)
  Private subnet:10.0.3.0/24  →  256 IPs (AZ-a)
  Private subnet:10.0.4.0/24  →  256 IPs (AZ-b)
```

> AWS reserves 5 IPs per subnet (first 4 + last 1)

---

## 🔒 Security Groups vs NACLs

| Feature | Security Group | NACL |
|---|---|---|
| Level | Instance | Subnet |
| State | Stateful | Stateless |
| Rules | Allow only | Allow + Deny |
| Evaluation | All rules evaluated | Rules evaluated in order (numbered) |
| Default | Deny all inbound, allow all outbound | Allow all |

---

## 🔒 Security best practices

- Always use multi-AZ subnets for high availability
- Keep databases in private subnets, never expose RDS to the internet
- Use VPC Endpoints for S3 and DynamoDB to avoid traffic going through internet
- Enable VPC Flow Logs for auditing and troubleshooting
- Use NAT Gateway (not NAT Instance) for production, it's managed and scalable
- Apply least privilege in Security Groups — never open 0.0.0.0/0 to sensitive ports

---

## 🏛️ Architect's view, typical 3-tier architecture

```
Internet
    │
Internet Gateway
    │
┌─────────────────────────┐
│  Public Subnet (AZ-a)   │  ← Load Balancer
└─────────────────────────┘
    │
┌─────────────────────────┐
│  Private Subnet (AZ-a)  │  ← App Servers (EC2)
└─────────────────────────┘
    │
┌─────────────────────────┐
│  Private Subnet (AZ-a)  │  ← Database (RDS)
└─────────────────────────┘
```

---

## 🔗 Integrates with

`EC2` `RDS` `Lambda` `ELB` `NAT Gateway` `Route 53` `Direct Connect` `VPN`

---

## ❓ Exam tips (SAA-C03)

- Default VPC is created automatically in every region, has public subnets
- VPC Peering is **non-transitive**, A↔B and B↔C does NOT mean A↔C
- **AWS Transit Gateway** solves the transitive peering problem at scale
- Security Groups are **stateful**, return traffic is automatically allowed
- NACLs are **stateless**, you must define both inbound AND outbound rules
- NAT Gateway must be in a **public subnet** and needs an Elastic IP

---

## 📎 References

- [VPC Official Docs](https://docs.aws.amazon.com/vpc/)
- [VPC CIDR Calculator](https://cidr.xyz/)
- [AWS VPC Subnet Design](https://aws.amazon.com/answers/networking/aws-single-vpc-design/)

---

*Last updated: March 2026*
