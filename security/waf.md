# WAF, Web Application Firewall

> Protects web applications from common exploits and attacks at the HTTP layer.

---

## 🧠 What it is
AWS WAF is a web application firewall that monitors and controls HTTP/HTTPS requests reaching your application. It works at Layer 7 (application layer) and lets you define rules to allow, block, or count requests based on conditions.

---

## 🔑 Key concepts

| Concept | Description |
|---|---|
| Web ACL | The main WAF resource, contains all your rules |
| Rule | A condition that inspects requests and takes an action |
| Rule Group | A reusable set of rules (AWS Managed or custom) |
| IP Set | A list of IP addresses to allow or block |
| Regex Set | Pattern matching on request components |
| Capacity Units (WCU) | Measures the processing cost of rules |
| Managed Rules | Pre-built rule groups maintained by AWS or partners |

---

## 🔍 What WAF can inspect

| Component | Examples |
|---|---|
| IP address | Block a specific IP or range |
| Country | Geo-block requests from certain countries |
| HTTP headers | Block requests with suspicious User-Agent |
| URI / query string | Block SQL injection attempts in URL params |
| Request body | Block XSS payloads in POST body |
| HTTP method | Allow only GET and POST |

---

## 🛡️ AWS Managed Rule Groups

| Rule Group | Protects against |
|---|---|
| Core rule set (CRS) | OWASP Top 10, XSS, SQLi, etc. |
| Known bad inputs | Exploits targeting Log4j, Spring, etc. |
| Amazon IP reputation | Known malicious IPs and bots |
| Bot Control | Scrapers, crawlers, credential stuffing |
| SQL database | SQL injection attacks |
| Linux / Windows | OS-specific exploits |

---

## ⚡ Rule actions

| Action | Behavior |
|---|---|
| Allow | Let the request through |
| Block | Return 403 Forbidden |
| Count | Log without blocking, use for testing |
| CAPTCHA | Challenge the user with a CAPTCHA |
| Challenge | Silent bot challenge (JS token verification) |

---

## 🔒 Security best practices

- Start in **Count mode** to test rules before switching to Block
- Always enable the **Core Rule Set (CRS)** as a baseline
- Add **Bot Control** for public-facing apps
- Use **rate-based rules** to limit requests per IP (L7 DDoS protection)
- Enable **WAF logging** to CloudWatch Logs or S3
- Review **sampled requests** regularly to tune false positives

---

## 🏛️ Architect's view — where WAF fits

```
Internet → Route 53 → CloudFront ← WAF (global)
                           │
                          ALB ← WAF (regional)
                           │
                    EC2 / ECS / Lambda
```

**Deploy WAF on:**
- **CloudFront**, global protection, closer to the attacker
- **Application Load Balancer (ALB)**, regional protection
- **API Gateway**, REST/HTTP API protection
- **AppSync**, GraphQL API protection
- **Cognito User Pools**, login endpoint protection

---

## WAF vs other AWS security services

| Service | Protects against | Layer |
|---|---|---|
| WAF | Application exploits (SQLi, XSS, bots) | L7 |
| Shield Standard | DDoS, automatically included | L3/L4 |
| Shield Advanced | Large-scale DDoS + WAF integration | L3/L4/L7 |
| Security Groups | Unauthorized network access | L4 |
| GuardDuty | Threat detection from logs/behavior | All |

---

## 🔗 Integrates with

`CloudFront` `ALB` `API Gateway` `AppSync` `Cognito` `CloudWatch` `Firewall Manager` `Shield`

---

## ❓ Exam tips (SAA-C03)

- WAF operates at **Layer 7**, cannot block L3/L4 DDoS (use Shield)
- WAF on CloudFront is **global**, always deployed in us-east-1
- WAF on ALB/API Gateway is **regional**
- **Rate-based rules** = WAF mechanism for basic L7 DDoS protection
- **AWS Firewall Manager** manages WAF rules centrally across accounts
- WAF does NOT replace Security Groups — they work at different layers

---

## 📎 References

- [WAF Official Docs](https://docs.aws.amazon.com/waf/)
- [AWS Managed Rules list](https://docs.aws.amazon.com/waf/latest/developerguide/aws-managed-rule-groups-list.html)
- [WAF Pricing](https://aws.amazon.com/waf/pricing/)

---

*Last updated: March 2026*
