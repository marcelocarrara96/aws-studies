# IAM — Identity and Access Management

> Controls WHO can do WHAT on which AWS resources. The foundation of every secure AWS architecture.

---

## 🧠 What it is
IAM lets you manage access to AWS services and resources securely. You create users, groups, roles and policies to control who can do what — and from where.

---

## 🔑 Key concepts

| Concept | Description |
|---|---|
| User | An individual identity (person or application) with credentials |
| Group | A collection of users that share the same permissions |
| Role | An identity assumed temporarily by a user, service, or application |
| Policy | A JSON document that defines permissions (Allow/Deny) |
| Permission Boundary | Limits the maximum permissions a user or role can have |
| Access Key | Programmatic credentials (CLI/SDK) — avoid when possible |
| MFA | Multi-Factor Authentication — adds a second layer of security |

---

## 📄 Policy structure

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::my-bucket/*"
    }
  ]
}
```

| Field | Description |
|---|---|
| Effect | `Allow` or `Deny` |
| Action | AWS API operation (e.g. `s3:PutObject`, `ec2:*`) |
| Resource | ARN of the resource the action applies to |
| Condition | Optional — adds conditions like IP, time, MFA |

---

## 🏛️ Policy types

| Type | Description |
|---|---|
| AWS Managed | Pre-built by AWS, maintained automatically |
| Customer Managed | Created by you, reusable across identities |
| Inline | Attached directly to one user/group/role — avoid when possible |
| Resource-based | Attached to the resource (e.g. S3 bucket policy) |
| SCPs | Service Control Policies — used in AWS Organizations |

---

## 🔒 Security best practices

- Enable MFA for root account and all human users
- Never use root account for daily tasks
- Grant least privilege — start with minimum permissions
- Use IAM Roles for EC2 instances instead of access keys
- Rotate access keys regularly (or avoid them entirely with roles)
- Use IAM Access Analyzer to detect overly permissive policies
- Set a strong password policy for all users

---

## 🏛️ Architect's view — when to use what

**IAM Users** → Human identities or legacy apps that don't support roles

**IAM Roles** → EC2 instances, Lambda functions, cross-account access, federated identity (SSO)

**IAM Groups** → Organize users by job function (Developers, Admins, ReadOnly)

**Resource-based policies** → When you need to grant cross-account access to a specific resource

> 💡 Prefer Roles over Users whenever possible. Roles don't have long-lived credentials.

---

## 🔗 Integrates with

`EC2` `Lambda` `S3` `RDS` `CloudTrail` `AWS Organizations` `SSO` `STS`

---

## ❓ Exam tips (SAA-C03)

- IAM is **global** — not tied to a region
- **Explicit Deny always wins** over any Allow
- **STS (Security Token Service)** issues temporary credentials for assumed roles
- **IAM Access Advisor** shows last-used permissions — useful for reducing scope
- Policies attached to a Group apply to all users in the group
- Root account has full access and **cannot be restricted by SCPs**

---

## 📎 References

- [IAM Official Docs](https://docs.aws.amazon.com/iam/)
- [IAM Best Practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html)
- [Policy Simulator](https://policysim.aws.amazon.com/)

---

*Last updated: March 2026*
