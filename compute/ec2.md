# EC2, Elastic Compute Cloud

> Virtual servers in the cloud. The backbone of most AWS architectures.

---

## 🧠 What it is
EC2 lets you rent virtual machines (instances) on AWS. You choose the OS,
CPU, memory, storage and networking. You pay by the hour or second.

---

## 🔑 Key concepts

| Concept | Description |
|---|---|
| Instance | A virtual machine running in AWS |
| AMI | Amazon Machine Image, the "template" used to launch an instance |
| Instance type | Defines CPU, RAM and network (ex: t3.micro, m5.large) |
| Security Group | Virtual firewall, controls inbound/outbound traffic |
| Key Pair | SSH credentials to access the instance |
| Elastic IP | Static public IP address you can attach to an instance |
| User Data | Script that runs automatically when instance launches |

---

## 🏗️ Instance type families

| Family | Optimized for | Example use case |
|---|---|---|
| t3, t4g | General / burstable | Dev environments, low-traffic apps |
| m6i, m7g | Balanced | Web servers, small databases |
| c6i, c7g | Compute | APIs, batch processing, video encoding |
| r6i, r7g | Memory | Databases, caching, data analytics |
| i3, i4i | Storage (NVMe) | High I/O databases, Hadoop |
| p3, g4 | GPU | Machine learning, rendering |

---

## 💰 Pricing models

| Model | Best for | Savings vs On-Demand |
|---|---|---|
| On-Demand | Unpredictable workloads, testing | - |
| Reserved (1 or 3 yr) | Steady, predictable workloads | up to 72% |
| Savings Plans | Flexible reserved alternative | up to 66% |
| Spot | Fault-tolerant, flexible workloads | up to 90% |
| Dedicated Host | Compliance / licensing requirements | - |

---

## 🔒 Security best practices

- Never open port 22 (SSH) to 0.0.0.0/0 - restrict to your IP
- Use IAM roles on instances instead of storing access keys
- Enable termination protection on production instances
- Use Security Groups as stateful firewalls (prefer over NACLs for most cases)
- Store secrets in AWS Secrets Manager, not in User Data scripts

---

## 🏛️ Architect's view, when to use EC2

**Use EC2 when:**
- You need full control over the OS or runtime
- Running legacy applications that can't be containerized
- Lift-and-shift migration from on-premises

**Prefer Lambda when:**
- Short-lived, event-driven tasks (under 15 min)
- You want zero server management

**Prefer ECS/EKS when:**
- Running containerized microservices at scale

---

## 🔗 Integrates with

`VPC` `IAM` `EBS` `ELB` `Auto Scaling` `CloudWatch` `S3` `RDS`

---

## ❓ Exam tips (SAA-C03)

- t2/t3 instances use **CPU credits** — know how burstable performance works
- Spot instances can be **interrupted** with 2 minutes notice
- Reserved Instances are a **billing concept**, not a reservation of physical hardware
- **Placement groups**: Cluster (low latency) vs Spread (high availability) vs Partition (Hadoop/Kafka)

---

## 📎 References

- [EC2 Official Docs](https://docs.aws.amazon.com/ec2/)
- [EC2 Instance Types](https://aws.amazon.com/ec2/instance-types/)
- [EC2 Pricing](https://aws.amazon.com/ec2/pricing/)

---

*Last updated: March 2026*
