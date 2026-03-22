# RDS, Relational Database Service

> Managed relational databases in the cloud. AWS handles backups, patching, failover and scaling.

---

## 🧠 What it is
RDS lets you run relational databases without managing the underlying infrastructure. AWS handles OS patching, backups, monitoring, and failover, you focus on your schema and queries.

---

## 🔑 Key concepts

| Concept | Description |
|---|---|
| DB Instance | The compute + storage unit running your database |
| DB Subnet Group | Set of subnets (multi-AZ) where RDS can be deployed |
| Parameter Group | Configuration settings for the database engine |
| Option Group | Additional features for specific engines (e.g. Oracle) |
| Read Replica | Read-only copy of the DB, for scaling reads |
| Multi-AZ | Standby replica in another AZ, for high availability |
| Snapshot | Manual or automated backup of the DB |
| Maintenance Window | Scheduled time for patches and upgrades |

---

## 🗄️ Supported engines

| Engine | Best for |
|---|---|
| MySQL | Web apps, open-source projects |
| PostgreSQL | Complex queries, GIS, JSON |
| MariaDB | MySQL-compatible, community-driven |
| Oracle | Enterprise legacy systems |
| SQL Server | Windows/.NET environments |
| Amazon Aurora | High performance MySQL/PostgreSQL, AWS-native |

---

## ⚡ RDS vs Aurora

| Feature | RDS | Aurora |
|---|---|---|
| Performance | Standard | Up to 5x MySQL, 3x PostgreSQL |
| Storage | Fixed provisioned | Auto-scales up to 128 TB |
| Replicas | Up to 5 read replicas | Up to 15 read replicas |
| Failover | 1-2 minutes | Under 30 seconds |
| Cost | Lower | Higher — worth it for production |

---

## 🔒 Security best practices

- Always deploy RDS in a **private subnet**, never expose to the internet
- Use **Security Groups** to restrict access to app servers only
- Enable **encryption at rest** using KMS
- Enable **encryption in transit** (SSL/TLS) for all connections
- Use **IAM Database Authentication** instead of hardcoded passwords
- Store credentials in **AWS Secrets Manager**, not in environment variables
- Enable **automated backups** with a retention period of at least 7 days

---

## 💰 Pricing models

| Model | Description |
|---|---|
| On-Demand | Pay per hour, good for dev/test |
| Reserved (1 or 3 yr) | Up to 60% savings, for steady production workloads |
| Multi-AZ | ~2x the cost of single-AZ, worth it for production |

---

## 🏛️ Architect's view

**Use RDS when:**
- You need SQL, ACID transactions, or complex joins
- Migrating an existing relational DB from on-premises
- Your team already knows MySQL/PostgreSQL

**Use Aurora when:**
- You need high throughput and availability in production
- You want seamless auto-scaling storage

**Use DynamoDB instead when:**
- You need massive scale with simple key-value or document queries
- You don't need SQL or complex joins

---

## 🔗 Integrates with

`VPC` `IAM` `KMS` `CloudWatch` `Secrets Manager` `Lambda` `EC2` `Aurora`

---

## ❓ Exam tips (SAA-C03)

- **Multi-AZ** = high availability (automatic failover, same region)
- **Read Replica** = performance / scalability (async replication, can be cross-region)
- Multi-AZ standby **cannot** be used for reads, it's only for failover
- RDS **automated backups** are enabled by default (1-day retention)
- Snapshots are **manual** and kept until you delete them
- **RDS Proxy** improves Lambda → RDS performance by pooling connections

---

## 📎 References

- [RDS Official Docs](https://docs.aws.amazon.com/rds/)
- [Aurora Docs](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/)
- [RDS Pricing](https://aws.amazon.com/rds/pricing/)

---

*Last updated: March 2026*
