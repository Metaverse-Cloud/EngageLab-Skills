# EngageLab Skills

This project maintains various EngageLab skills.

- [x] Email
- [x] SMS
- [x] OTP
- [x] WhatsApp Business API
- [ ] Silent Auth
- [ ] CAPTCHA

## Email

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


## SMS

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
├── scripts/
│   └── sms_client.py                          # Python client for all SMS API endpoints
└── references/
    ├── template-and-signature-api.md          # Detailed CRUD API specs
    └── error-codes.md                         # Error code reference
```

| File | Purpose |
|------|---------|
| `SKILL.md` | Entry point — authentication, endpoint overview, sending workflow, template & signature CRUD summaries, code generation guidance |
| `scripts/sms_client.py` | Python client class (`EngageLabSMS`) wrapping all endpoints: send SMS (immediate/scheduled), template CRUD, and signature CRUD |
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

## OTP

An agent skill that enables AI assistants to interact with the [EngageLab OTP REST API](https://www.engagelab.com/docs/OTP/Product-Overview). It handles one-time password generation, multi-channel delivery (SMS, WhatsApp, Email, Voice), verification, custom messaging, template management, callback webhooks, and SMPP integration.

### What It Does

- **Send OTP** — Generate and deliver one-time passwords via the platform, or send your own custom codes
- **Verify OTP** — Validate verification codes submitted by users
- **Custom Messages** — Send verification codes, notifications, and marketing content using custom templates
- **Manage Templates** — Create, list, get, and delete OTP templates with multi-channel fallback strategies
- **Callback Configuration** — Set up webhooks to receive delivery status, notification events, and system events
- **SMPP Integration** — Connect via SMPP protocol for carrier-level SMS delivery

### Installation

```shell
npx skills add https://github.com/Metaverse-Cloud/EngageLab-Skills/tree/main/engagelab-otp
```

### Skill Structure

```
engagelab-otp/
├── SKILL.md                                   # Main skill file
├── scripts/
│   ├── otp_client.py                          # Python client for all OTP API endpoints
│   └── verify_callback.py                     # HMAC signature verifier for callback webhooks
└── references/
    ├── error-codes.md                         # Error code reference
    ├── template-api.md                        # Template CRUD API specs
    ├── callback-config.md                     # Callback webhook configuration
    └── smpp-guide.md                          # SMPP protocol integration guide
```

| File | Purpose |
|------|---------|
| `SKILL.md` | Entry point — authentication, endpoint overview, OTP send/verify workflow, custom messages, template management summary, code generation guidance |
| `scripts/otp_client.py` | Python client class (`EngageLabOTP`) wrapping all endpoints: send OTP, custom OTP, verify, custom messages, and template CRUD |
| `scripts/verify_callback.py` | HMAC-SHA256 signature verifier for incoming OTP callback webhooks — drop into Flask/FastAPI/Django |
| `references/error-codes.md` | Complete error code tables for OTP sending, verification, and template operations |
| `references/template-api.md` | Full request/response specs for template CRUD including WhatsApp, SMS, Voice, Email, and PWA channel configurations |
| `references/callback-config.md` | Webhook URL setup, HMAC signature security, and all event types (message status, notifications, uplink messages, system events) |
| `references/smpp-guide.md` | SMPP connection setup, message sending, delivery reports, keep-alive, and status codes |

### API Coverage

| Operation | Method | Endpoint |
|-----------|--------|----------|
| Send OTP (platform-generated) | `POST` | `/v1/messages` |
| Send OTP (custom code) | `POST` | `/v1/codes` |
| Verify OTP | `POST` | `/v1/verifications` |
| Send custom message | `POST` | `/v1/custom-messages` |
| List templates | `GET` | `/v1/template-configs` |
| Get template details | `GET` | `/v1/template-configs/:templateId` |
| Create template | `POST` | `/v1/template-configs` |
| Delete template | `DELETE` | `/v1/template-configs/:templateId` |

### Prerequisites

Before using this skill, complete these steps in the [EngageLab console](https://www.engagelab.com):

1. **Create API credentials** — Go to Configuration Management > API Keys to generate a `dev_key` and `dev_secret`
2. **Set up OTP templates** — Create templates with channel strategies (e.g., WhatsApp → SMS fallback) and submit for review
3. **Configure callback URL** (optional) — Set up a webhook endpoint to receive delivery status and event notifications

### Authentication

All API calls use HTTP Basic Authentication:

```
Authorization: Basic base64(dev_key:dev_secret)
```

The API base URL is `https://otp.api.engagelab.cc`.

## WhatsApp Business API

An agent skill that enables AI assistants to interact with the [EngageLab WhatsApp Business REST API](https://www.engagelab.com/whatsapp-business-api). As a Meta-authorized WhatsApp Business solution provider, EngageLab connects businesses with over 2 billion WhatsApp users for marketing, notifications, OTP verification, and customer service.

### What It Does

- **Send Messages** — Deliver template, text, image, video, audio, document, and sticker messages via WhatsApp
- **Manage Templates** — Create, list, get, update, and delete WABA message templates with header/body/footer/button components
- **Handle Callbacks** — Receive message delivery status, user responses (replies, orders), and system notifications (balance, template updates, WABA events)

### Installation

```shell
npx skills add https://github.com/Metaverse-Cloud/EngageLab-Skills/tree/main/engagelab-whatsapp-business
```

### Skill Structure

```
engagelab-whatsapp-business/
├── SKILL.md                                   # Main skill file
├── scripts/
│   └── whatsapp_client.py                     # Python client for all WhatsApp API endpoints
└── references/
    ├── error-codes.md                         # Error code reference
    ├── template-api.md                        # Template CRUD API specs with components object
    └── callback-api.md                        # Callback webhook events and data structures
```

| File | Purpose |
|------|---------|
| `SKILL.md` | Entry point — authentication, endpoint overview, all message types with examples, template management summary, callback events, code generation guidance |
| `scripts/whatsapp_client.py` | Python client class (`EngageLabWhatsApp`) wrapping all endpoints: 7 message types + template CRUD with filtering |
| `references/error-codes.md` | Complete error code tables for messaging and template APIs |
| `references/template-api.md` | Full template CRUD specs with components object details (header, body, footer, buttons) and language codes |
| `references/callback-api.md` | Webhook callback events: message status lifecycle, user responses, and system notifications |

### API Coverage

| Operation | Method | Endpoint |
|-----------|--------|----------|
| Send message | `POST` | `/v1/messages` |
| List templates | `GET` | `/v1/templates` |
| Get template | `GET` | `/v1/templates/:templateId` |
| Create template | `POST` | `/v1/templates` |
| Update template | `PUT` | `/v1/templates/:templateId` |
| Delete template | `DELETE` | `/v1/templates/:templateName` |

### Prerequisites

Before using this skill, complete these steps in the [EngageLab console](https://www.engagelab.com):

1. **Create API credentials** — Go to Configuration Management > API Keys to generate a `dev_key` (DevKey) and `dev_secret` (DevSecret)
2. **Apply for WhatsApp Business API** — Complete the onboarding process with EngageLab and Meta
3. **Configure a sending number** — Set up your WhatsApp Business phone number in the console
4. **Create message templates** — Submit templates for Meta review before sending proactive messages

### Authentication

All API calls use HTTP Basic Authentication:

```
Authorization: Basic base64(dev_key:dev_secret)
```

The API base URL is `https://wa.api.engagelab.cc`.
