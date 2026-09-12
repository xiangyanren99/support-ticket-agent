# Create Northstar Support Ticket Flow

## Purpose

Create a structured support ticket in Microsoft Dataverse and return the generated ticket reference to the Copilot Studio agent.

## Trigger

**When an agent calls the flow**

### Inputs

| Input | Type | Purpose |
|---|---|---|
| `issue_category` | Text | Standardized issue classification |
| `issue_description` | Text | Concise description of the technical problem |
| `urgency` | Text | User-provided technical support urgency |
| `requester_email` | Text | Email associated with the requester |
| `troubleshooting_attempted` | Text | Summary of troubleshooting already performed |

### Supported Issue Categories

- Synchronization
- Offline Access
- Schedule
- Application Error
- Other

### Supported Urgency Values

- Low
- Medium
- High

No category or urgency is silently assigned when the required information is missing.

## Flow

### 1. Generate Ticket Reference

A Compose action generates the human-readable ticket reference:

`concat('NST-', formatDateTime(utcNow(),'yyyyMMddHHmmss'))`

Example:

`NST-20260820074339`

The timestamp approach is sufficient for this portfolio prototype but is not intended as a production-grade uniqueness strategy.

### 2. Map Issue Category

A Switch maps the incoming `issue_category` value to its corresponding Dataverse Choice value.

Supported branches:

- Synchronization
- Offline Access
- Schedule
- Application Error
- Other

### 3. Map Urgency

A second Switch maps `urgency` to the corresponding Dataverse Choice value.

Supported branches:

- Low
- Medium
- High

There is no default urgency branch. If urgency is unavailable, the agent must obtain it before ticket creation.

### 4. Create Dataverse Record

**Connector:** Microsoft Dataverse  
**Action:** Add a new row  
**Table:** Support Tickets

Mappings:

| Dataverse field | Source |
|---|---|
| Ticket Reference | Generated ticket reference |
| Issue Category | Mapped category Choice |
| Issue Description | `issue_description` |
| Urgency | Mapped urgency Choice |
| Requester Email | `requester_email` |
| Troubleshooting Attempted | `troubleshooting_attempted` |
| Ticket Status | Open |

### 5. Respond to Agent

The flow returns:

- `ticket_reference`
- `status`

Example:

`ticket_reference = NST-20260820074339`

`status = Ticket created successfully`

## Tool Configuration

The published flow is attached to the Northstar Mobile Support Agent as the **Create Support Ticket** tool.

User confirmation is required before execution because the tool performs a write operation.

## Result

Successful execution creates a structured Dataverse Support Ticket record and returns the same ticket reference to the conversational agent.