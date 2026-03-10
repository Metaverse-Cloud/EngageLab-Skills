# EngageLab Skills

This project maintains various EngageLab skills.

- [x] Email
- [x] SMS
- [ ] OTP
- [ ] WhatsApp

## EngageLab Email Skill

An agent skill that enables AI assistants to send emails via the [EngageLab Email REST API](https://www.engagelab.com/email). It supports plain sending, variable substitution (`%var%` and `{{var}}`), Base64-encoded attachments, and advanced settings such as sandbox mode, open/click/unsubscribe tracking.

### What It Does

- **Send Email** — Send HTML or plain-text emails with CC, BCC, and reply-to support
- **Variable Substitution** — Personalize subject and body with `vars` (`%name%`) or `dynamic_vars` (`{{name}}`) for batch campaigns
- **Attachments** — Attach Base64-encoded files as regular attachments or inline images
- **Advanced Settings** — Configure send mode (plain / template / address-list), sandbox testing, and tracking (open, click, unsubscribe)

### Installation

```shell
npx skills add https://github.com/Metaverse-Cloud/EngageLab-Skills/tree/main/engagelab-email
```

### Skill Structure

```
engagelab-email/
├── SKILL.md                                    # Main skill file
├── scripts/
│   └── send_email.py                           # Ready-to-use Python helper for sending emails
├── references/
│   └── api_spec.md                             # Full REST API parameter spec & examples
└── templates/
    └── email_request_template.json             # Sample request body for quick start
```

| File | Purpose |
|------|---------|
| `SKILL.md` | Entry point — overview, core features, variable substitution patterns, attachment handling, settings reference |
| `scripts/send_email.py` | Python function wrapping authentication, payload construction, and error handling for `/v1/mail/send` |
| `references/api_spec.md` | Comprehensive API field specs, request examples, and response formats |
| `templates/email_request_template.json` | JSON template showing all available fields with sandbox mode enabled |

### API Coverage

| Operation | Method | Endpoint |
|-----------|--------|----------|
| Send email | `POST` | `/v1/mail/send` |

### Prerequisites

Before using this skill, complete these steps in the [EngageLab console](https://www.engagelab.com):

1. **Create API credentials** — Go to Configuration Management > API Keys to generate an `api_user` and `api_key`
2. **Verify a sender domain** — Configure and verify your sending domain so emails are delivered properly
3. **Set up labels** (optional) — Create labels to categorize and track different email campaigns

### Authentication

All API calls use HTTP Basic Authentication:

```
Authorization: Basic base64(api_user:api_key)
```

The default data center endpoint is `https://email.api.engagelab.cc` (Singapore).


## EngageLab SMS Skill

An agent skill that enables AI assistants to interact with the [EngageLab SMS REST API](https://www.engagelab.com/sms). It provides structured instructions for sending SMS messages and managing templates and sender ID signatures through EngageLab's platform.

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