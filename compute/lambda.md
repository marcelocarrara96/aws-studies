# Lambda, Serverless Functions

> Run code without managing servers. You pay only for what you use, per millisecond.

---

## 🧠 What it is
Lambda lets you run code in response to events, HTTP requests, file uploads, database changes, scheduled tasks, without provisioning or managing any servers. AWS handles everything: scaling, patching, availability.

---

## 🔑 Key concepts

| Concept | Description |
|---|---|
| Function | Your code + configuration (runtime, memory, timeout) |
| Trigger | The event source that invokes the function |
| Handler | The entry point of your function (e.g. `index.handler`) |
| Execution Role | IAM role that grants the function permissions |
| Layer | Shared code/dependencies packaged separately |
| Concurrency | Number of function instances running simultaneously |
| Cold Start | Delay when a new instance is initialized (first invocation) |
| Destination | Where to send results of async invocations (success/failure) |

---

## ⚙️ Configuration limits

| Setting | Default | Maximum |
|---|---|---|
| Timeout | 3 seconds | 15 minutes |
| Memory | 128 MB | 10,240 MB (10 GB) |
| Package size (zip)  | 50 MB (250 MB unzipped) |
| Ephemeral storage (/tmp) | 512 MB | 10,240 MB |
| Concurrency (per account) | 1,000 | Configurable (request increase) |

---

## 🔌 Common triggers

| Trigger | Use case |
|---|---|
| API Gateway | HTTP REST or WebSocket API |
| S3 | Process files on upload |
| DynamoDB Streams | React to DB changes |
| SQS | Process messages from a queue |
| EventBridge | Scheduled tasks (cron) or event-driven rules |
| SNS | Push notifications, fan-out patterns |
| CloudFront (Lambda@Edge) | Run code at edge locations |

---

## 💰 Pricing

- **Free tier:** 1M requests/month + 400,000 GB-seconds/month
- **Requests:** $0.20 per 1M requests after free tier
- **Duration:** charged per ms based on memory allocated

> Lambda is extremely cheap for low-to-medium traffic. At very high scale, compare with EC2/Fargate.

---

## 🔒 Security best practices

- Use execution roles with least privilege, only grant what the function needs
- Never hardcode credentials, use IAM roles + Secrets Manager
- Enable VPC access only when the function needs to reach private resources (RDS, ElastiCache)
- Use Lambda Layers for shared dependencies, keeps packages small and auditable
- Enable X-Ray tracing for observability and debugging
- Set reserved concurrency to prevent a function from consuming all account concurrency

---

## 🏛️ Architect's view

**Use Lambda when:**
- Event-driven, short-lived tasks (file processing, notifications, webhooks)
- Building APIs with API Gateway, fully serverless backend
- Scheduled jobs (replacing cron jobs on EC2)
- Reacting to changes in S3, DynamoDB, SQS

**Avoid Lambda when:**
- Tasks run longer than 15 minutes
- You need persistent connections at scale
- You need very predictable, high-frequency throughput (cold starts matter)

---

## 🧱 Serverless architecture pattern

```
User → API Gateway → Lambda → DynamoDB
                   ↓
              S3 / SES / SNS
```

---

## 🔗 Integrates with

`API Gateway` `S3` `DynamoDB` `SQS` `SNS` `EventBridge` `RDS Proxy` `VPC` `IAM` `X-Ray`

---

## ❓ Exam tips (SAA-C03)

- Lambda scales automatically, **one instance per concurrent request**
- **Cold start** is a concern for latency-sensitive apps, use Provisioned Concurrency to pre-warm
- Lambda inside a VPC needs a **NAT Gateway** to reach the internet
- **Lambda@Edge** runs at CloudFront edge locations, lower latency globally
- Max execution time is **15 minutes**, anything longer needs EC2, Fargate or Step Functions
- Use **SQS + Lambda** for decoupled, resilient async processing

---

## 📎 References

- [Lambda Official Docs](https://docs.aws.amazon.com/lambda/)
- [Lambda Pricing](https://aws.amazon.com/lambda/pricing/)
- [Serverless Land (patterns)](https://serverlessland.com/)

---

*Last updated: March 2026*
