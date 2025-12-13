# General Bots Templates

Pre-built templates for bots, apps, prompts, and UI components. Everything you need to get started quickly.

---

## Repository Structure

```
bottemplates/
├── bots/                    # Complete bot packages (.gbai)
│   ├── core/                # Essential starter bots
│   ├── sales/               # CRM, marketing, lead management
│   ├── compliance/          # LGPD, GDPR, HIPAA
│   ├── finance/             # Banking, payments, invoicing
│   ├── healthcare/          # Patient communication, appointments
│   ├── hr/                  # Employee management, onboarding
│   ├── it/                  # Helpdesk, IT service management
│   ├── nonprofit/           # Donor management, volunteers
│   ├── education/           # Courses, training, LMS
│   └── integration/         # External API integrations
├── apps/                    # HTMX web application templates
│   ├── dashboard/           # Analytics and KPI dashboards
│   ├── crud/                # Generic CRUD interfaces
│   ├── kanban/              # Board-style project management
│   ├── admin/               # Admin panel templates
│   └── components/          # Reusable UI components
├── prompts/                 # System prompts and LLM configurations
│   ├── assistants/          # Role-specific assistant prompts
│   ├── tools/               # Tool description templates
│   └── personas/            # Bot personality definitions
├── dialogs/                 # Reusable BASIC dialog scripts
│   ├── auth/                # Authentication flows
│   ├── notifications/       # Email, SMS, WhatsApp patterns
│   ├── data/                # CRUD operation patterns
│   └── integrations/        # API integration patterns
└── themes/                  # UI themes (.gbtheme)
    ├── default/             # Standard theme
    ├── dark/                # Dark mode theme
    └── corporate/           # Business-focused themes
```

---

## Quick Start

### Install a Bot Template

```bash
# From CLI
botserver --install-template crm

# Or copy manually
cp -r bottemplates/bots/sales/crm.gbai /path/to/your/packages/
```

### Use an App Template

```basic
' Generate a CRM app from template
CREATE SITE "my-crm", "bottemplates/apps/crud", "Build a customer management system"
```

### Apply a Prompt Template

```basic
' Load a sales assistant prompt
SET SYSTEM PROMPT FROM FILE "bottemplates/prompts/assistants/sales.md"
```

---

## Bots

Complete `.gbai` packages ready to deploy.

### Core

| Template | Description |
|----------|-------------|
| `default.gbai` | Minimal starter bot |
| `template.gbai` | Reference implementation for creating new bots |

### Sales & Marketing

| Template | Description |
|----------|-------------|
| `crm.gbai` | Full CRM with leads, contacts, opportunities |
| `marketing.gbai` | Campaign management, email sequences |
| `attendance-crm.gbai` | Event attendance tracking |

### Compliance

| Template | Description |
|----------|-------------|
| `privacy.gbai` | LGPD, GDPR, CCPA data subject rights |
| `hipaa-medical.gbai` | HIPAA/HITECH healthcare compliance |

### Finance

| Template | Description |
|----------|-------------|
| `bank.gbai` | Banking services bot |
| `invoicing.gbai` | Invoice generation and tracking |

### Platform

| Template | Description |
|----------|-------------|
| `analytics-dashboard.gbai` | Platform metrics and reports |
| `bi.gbai` | Business intelligence dashboards |
| `talk-to-data.gbai` | Natural language SQL queries |
| `backup.gbai` | Server backup automation |

### AI & LLM

| Template | Description |
|----------|-------------|
| `llm-server.gbai` | LLM model hosting |
| `llm-tools.gbai` | TOOL-based LLM examples |
| `ai-search.gbai` | AI-powered document search |

---

## Apps

HTMX web application templates for use with `CREATE SITE`.

### Dashboard Templates

```basic
CREATE SITE "metrics", "bottemplates/apps/dashboard", "
Executive dashboard with:
- Revenue KPI cards
- Monthly trend charts
- Top performers table
"
```

### CRUD Templates

```basic
CREATE SITE "contacts", "bottemplates/apps/crud", "
Contact management with:
- Searchable list view
- Add/edit forms
- Import/export buttons
"
```

### Kanban Templates

```basic
CREATE SITE "projects", "bottemplates/apps/kanban", "
Project board with:
- Drag and drop cards
- Status columns
- Assignee filtering
"
```

### Components

Reusable HTML components:

| Component | File | Description |
|-----------|------|-------------|
| Data Table | `data-table.html` | Sortable, filterable tables |
| Form Modal | `form-modal.html` | Modal dialog with form |
| KPI Card | `kpi-card.html` | Metric display card |
| Chart | `chart.html` | Chart.js container |
| Search | `search-filter.html` | Search with filters |

---

## Prompts

System prompts and LLM configuration templates.

### Assistant Prompts

| Prompt | Description |
|--------|-------------|
| `sales.md` | Sales assistant persona |
| `support.md` | Customer support agent |
| `analyst.md` | Data analyst assistant |
| `developer.md` | Technical assistant |

### Tool Templates

Templates for creating LLM-invokable tools:

```basic
' From bottemplates/dialogs/tools/template.bas
PARAM input AS STRING DESCRIPTION "Description of input"
DESCRIPTION "What this tool does. When to use it."

' Your tool logic here
result = PROCESS input
RETURN result
```

---

## Dialogs

Reusable BASIC script patterns.

### Authentication

```basic
' bottemplates/dialogs/auth/oauth-flow.bas
INCLUDE "bottemplates/dialogs/auth/oauth-flow.bas"
```

### Notifications

```basic
' Send multi-channel notification
INCLUDE "bottemplates/dialogs/notifications/multi-channel.bas"
NOTIFY user, "Your order shipped!", channels: ["email", "whatsapp"]
```

### Data Operations

```basic
' CRUD with validation
INCLUDE "bottemplates/dialogs/data/validated-crud.bas"
CREATE_VALIDATED "contacts", contact_data, validation_rules
```

---

## Themes

UI customization packages.

### Using a Theme

```
my-bot.gbai/
└── my-bot.gbtheme/    # Copy theme files here
    ├── colors.css
    ├── fonts.css
    └── components.css
```

### Available Themes

| Theme | Description |
|-------|-------------|
| `default` | Clean, modern appearance |
| `dark` | Dark mode with accent colors |
| `corporate` | Professional business styling |
| `minimal` | Stripped-down, fast-loading |

---

## Bot Package Structure

Every `.gbai` bot follows this structure:

```
my-bot.gbai/
├── README.md                 # Documentation
├── my-bot.gbdialog/          # BASIC scripts
│   ├── start.bas             # Entry point
│   └── tools/                # LLM-invokable tools
├── my-bot.gbot/              # Configuration
│   └── config.csv            # Bot settings
├── my-bot.gbkb/              # Knowledge base (optional)
│   └── docs/                 # Documents for RAG
├── my-bot.gbdrive/           # File storage (optional)
└── my-bot.gbtheme/           # UI customization (optional)
```

---

## Best Practices

### Event-Driven Design

Use `ON` triggers instead of polling:

```basic
' ✅ Good - Event-driven
ON INSERT OF "leads"
    lead = GET LAST "leads"
    NOTIFY sales_team, "New lead: " + lead.name
END ON

' ❌ Bad - Polling loop
mainLoop:
    leads = FIND "leads", "new = true"
    WAIT 5
GOTO mainLoop
```

### LLM-Invokable Tools

Add `PARAM` and `DESCRIPTION` to make scripts callable by LLM:

```basic
' score-lead.bas
PARAM email AS STRING LIKE "john@example.com" DESCRIPTION "Lead email"
PARAM company AS STRING DESCRIPTION "Company name"

DESCRIPTION "Score and qualify a sales lead"

score = AI SCORE LEAD email, company
RETURN score
```

### HTMX Patterns

Generated apps should use HTMX for server communication:

```html
<div hx-get="/api/data/leads"
     hx-trigger="load, every 30s"
     hx-swap="innerHTML">
    Loading...
</div>
```

---

## Contributing

1. Fork this repository
2. Create your template following the structure
3. Test thoroughly
4. Add documentation
5. Submit a pull request

### Template Checklist

- [ ] Follows naming conventions
- [ ] Includes README.md
- [ ] Uses event-driven patterns
- [ ] Has proper error handling
- [ ] Documented configuration options
- [ ] Example usage provided

---

## License

AGPL-3.0 - Part of General Bots Open Source Platform

---

**Pragmatismo** - [pragmatismo.com.br](https://pragmatismo.com.br)