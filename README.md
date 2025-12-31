# AI Security Assessment Framework

A structured methodology for assessing the security posture of AI/ML workloads on AWS, with a focus on generative AI services like Amazon Bedrock.

## The Problem

Organizations are rapidly adopting AI services — deploying Bedrock agents, building RAG pipelines, integrating LLMs into production workflows — often without adequate security review.

Security teams face new challenges:
- Traditional threat models don't fully apply to AI systems
- Prompt injection is an unsolved vulnerability class
- Data flows to and from models are poorly understood
- IAM permissions for AI services are often over-privileged
- Guardrails and content filtering are misconfigured or missing
- Logging and monitoring gaps leave blind spots

Compliance teams are asking questions no one can answer. This framework helps bridge that gap.

## What This Covers

### Core Assessment Areas

| Domain | Focus |
|--------|-------|
| **AI Service Configuration** | Bedrock model access, inference profiles, provisioned throughput security |
| **Identity & Access** | IAM policies for AI services, least privilege analysis, cross-account access |
| **Data Protection** | Training data exposure, RAG data sources, embedding storage, model I/O logging |
| **Guardrails & Filtering** | Content filters, denied topics, PII redaction, word filters, contextual grounding |
| **Agent Security** | Tool permissions, action group configurations, agent trust boundaries |
| **Logging & Monitoring** | CloudTrail coverage, model invocation logging, CloudWatch integration |
| **Network Security** | VPC configurations, PrivateLink usage, egress controls |
| **Prompt Security** | Injection vectors, system prompt exposure, indirect injection via RAG |

### AWS Services in Scope

- Amazon Bedrock (Models, Agents, Knowledge Bases, Guardrails)
- Amazon SageMaker (where applicable)
- Supporting services: IAM, KMS, CloudTrail, CloudWatch, S3, OpenSearch Serverless

## Methodology

```
┌─────────────────────────────────────────────────────────────────┐
│  1. DISCOVERY                                                    │
│     - Inventory AI/ML workloads and services                    │
│     - Map data flows (inputs, outputs, training data)           │
│     - Identify integration points and trust boundaries          │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│  2. CONFIGURATION REVIEW                                         │
│     - IAM policy analysis                                        │
│     - Service configurations against security baselines          │
│     - Encryption settings (at rest, in transit)                 │
│     - Network architecture                                       │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│  3. THREAT ANALYSIS                                              │
│     - Prompt injection vectors                                   │
│     - Data leakage paths                                         │
│     - Privilege escalation via AI agents                        │
│     - Model abuse scenarios                                      │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│  4. GUARDRAILS EVALUATION                                        │
│     - Content filtering effectiveness                            │
│     - PII handling                                               │
│     - Denied topics coverage                                     │
│     - Bypass testing                                             │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│  5. REPORTING                                                    │
│     - Findings with severity ratings                            │
│     - Evidence and reproduction steps                           │
│     - Prioritized remediation guidance                          │
│     - Compliance mapping (where applicable)                     │
└─────────────────────────────────────────────────────────────────┘
```

## Repository Structure

```
.
├── README.md
├── methodology/
│   ├── discovery-checklist.md
│   ├── configuration-review.md
│   ├── threat-analysis.md
│   └── guardrails-testing.md
├── checklists/
│   ├── bedrock-security-checklist.md
│   ├── iam-review-checklist.md
│   ├── logging-checklist.md
│   └── agent-security-checklist.md
├── scripts/
│   ├── bedrock-config-audit.py
│   ├── iam-policy-analyzer.py
│   └── guardrails-export.py
├── templates/
│   ├── assessment-report-template.md
│   ├── findings-template.md
│   └── executive-summary-template.md
├── references/
│   ├── owasp-llm-top10-mapping.md
│   ├── aws-security-best-practices.md
│   └── compliance-control-mapping.md
└── examples/
    └── sample-findings/
```

## Threat Model Reference

This framework aligns with industry standards:

- **OWASP LLM Top 10** — Prompt injection, data leakage, insecure output handling, etc.
- **MITRE ATLAS** — Adversarial threat landscape for AI systems
- **AWS Well-Architected (Security Pillar)** — Cloud security best practices
- **NIST AI RMF** — AI risk management considerations

## Getting Started

### Prerequisites

- AWS CLI configured with appropriate permissions
- Python 3.9+
- boto3

### Installation

```bash
git clone https://github.com/[your-username]/ai-security-assessment.git
cd ai-security-assessment
pip install -r requirements.txt
```

### Running an Assessment

```bash
# Export Bedrock configurations
python scripts/bedrock-config-audit.py --profile your-aws-profile --region eu-west-1

# Analyze IAM policies for AI services
python scripts/iam-policy-analyzer.py --profile your-aws-profile

# Review guardrails configuration
python scripts/guardrails-export.py --profile your-aws-profile --region eu-west-1
```

## Sample Findings

| ID | Severity | Finding |
|----|----------|---------|
| AI-001 | High | Bedrock model invocation logging disabled — no visibility into prompts/responses |
| AI-002 | High | Agent action group allows `s3:*` on sensitive buckets |
| AI-003 | Medium | No guardrails attached to production Bedrock agent |
| AI-004 | Medium | Knowledge base data source uses overly permissive IAM role |
| AI-005 | Low | Guardrails content filter set to LOW strength |

## Roadmap

- [x] Initial methodology documentation
- [ ] Bedrock configuration audit scripts
- [ ] IAM policy analyzer for AI services
- [ ] Guardrails testing toolkit
- [ ] Automated report generation
- [ ] Terraform/CloudFormation compliance checks
- [ ] SageMaker assessment module
- [ ] Multi-cloud expansion (Azure OpenAI, GCP Vertex AI)

## Contributing

Contributions welcome. Please open an issue to discuss proposed changes before submitting a PR.

Areas where help is needed:
- Additional detection rules for AI-specific threats
- Compliance framework mappings (SOC 2, ISO 27001, GDPR)
- Testing methodologies for prompt injection

## References

- [OWASP LLM Top 10](https://owasp.org/www-project-top-10-for-large-language-model-applications/)
- [MITRE ATLAS](https://atlas.mitre.org/)
- [AWS Bedrock Security Documentation](https://docs.aws.amazon.com/bedrock/latest/userguide/security.html)
- [AWS Well-Architected Framework — Security Pillar](https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/welcome.html)

## License

MIT License — see [LICENSE](LICENSE) for details.

## About

Built by a Cloud Security Engineer focused on AWS security and the emerging intersection of cloud infrastructure and AI systems.

- AWS Security Specialty Certified
- Background in cloud security architecture, detection engineering, and security automation

---

*This framework is a work in progress. Star the repo to follow updates.*
