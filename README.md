# EngageLab Skills

This project maintains various EngageLab skills.

## EngageLab SMS Skill

An agent skill that enables AI assistants to interact with the [EngageLab SMS REST API](https://www.engagelab.com). It provides structured instructions for sending SMS messages and managing templates and sender ID signatures through EngageLab's platform.

### What It Does

- **Send SMS** — Compose and send notification or marketing SMS to one or more recipients using pre-approved templates
- **Manage Templates** — Create, list, update, and delete SMS templates (with variable placeholders and review workflow)
- **Manage Signatures (Sender IDs)** — Create, list, update, and delete sender ID signatures attached to templates

### Installation

```shell
npx skills add https://github.com/Metaverse-Cloud/EngageLab-Skills/tree/main/engagelab-sms
```

### Skill Structure

```
engagelab-sms/
├── SKILL.md                                   # Main skill file
└── references/
    ├── template-and-signature-api.md          # Detailed CRUD API specs
    └── error-codes.md                         # Error code reference
```

| File | Purpose |
|------|---------|
| `SKILL.md` | Entry point — authentication, endpoint overview, sending workflow, template & signature CRUD summaries, code generation guidance |
| `references/template-and-signature-api.md` | Full request/response field specs for all template and signature endpoints |
| `references/error-codes.md` | Complete error code tables for SMS sending and template/signature operations |

### API Coverage

| Operation | Method | Endpoint |
|-----------|--------|----------|
| Send SMS | `POST` | `/v1/messages` |
| List templates | `GET` | `/v1/template-configs` |
| Get template | `GET` | `/v1/template-configs/:templateId` |
| Create template | `POST` | `/v1/template-configs` |
| Update template | `PUT` | `/v1/template-configs/:templateId` |
| Delete template | `DELETE` | `/v1/template-configs/:templateId` |
| List signatures | `GET` | `/v1/sign-configs` |
| Get signature | `GET` | `/v1/sign-configs/:signId` |
| Create signature | `POST` | `/v1/sign-configs` |
| Update signature | `PUT` | `/v1/sign-configs/:signId` |
| Delete signature | `DELETE` | `/v1/sign-configs/:signId` |

### Prerequisites

Before using this skill, complete these steps in the [EngageLab console](https://www.engagelab.com):

1. **Create an API key** — Go to Configuration Management > API Keys to generate a `dev_key` and `dev_secret`
2. **Set up SMS templates** — Go to Message Center > Template Management to create and submit templates for review
3. **Configure sender IDs** (optional) — Create signature configurations to identify the sender

### Authentication

All API calls use HTTP Basic Authentication:

```
Authorization: Basic base64(dev_key:dev_secret)
```