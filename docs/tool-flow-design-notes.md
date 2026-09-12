# Tool and Flow Design Notes

## Objective

The Northstar Mobile Support Agent helps users troubleshoot fictional Northstar Visit Mobile issues and creates a structured support ticket when technical support is required.

The project demonstrates how an AI agent can move beyond question answering and safely perform a business action through a tool.

## Design Approach

The solution separates conversational reasoning from deterministic business logic.

The Copilot Studio agent is responsible for understanding the user's request, retrieving troubleshooting guidance, gathering required information, and deciding when ticket creation is appropriate.

The Create Support Ticket tool invokes an agent flow that performs the actual database write.

This separation keeps natural-language reasoning in the agent while keeping the business action predictable and structured.

## Component Responsibilities

### Copilot Studio Agent

The agent:

- Interprets the user's request.
- Uses the configured Northstar knowledge source for troubleshooting.
- Determines whether a support ticket is needed.
- Collects missing tool inputs.
- Classifies the issue into an approved category.
- Requests confirmation before ticket creation.
- Communicates the result back to the user.

### Create Support Ticket Tool

The tool exposes ticket creation as a capability available to the agent.

The agent decides when the tool should be invoked, but the tool performs the action through the associated agent flow.

### Agent Flow

The Create Northstar Support Ticket flow performs the ticket creation process.

It:

1. Receives structured inputs from the agent.
2. Generates a human readable ticket reference.
3. Maps issue category and urgency to Dataverse Choice values.
4. Creates a Support Tickets row in Dataverse.
5. Returns the generated ticket reference and status to the agent.

### Dataverse Connector

The Microsoft Dataverse connector provides authenticated communication between the agent flow and Dataverse.

### Dataverse

Dataverse provides persistent structured storage for the support-ticket records.

## Structured Tool Inputs

The tool receives:

- `issue_category`
- `issue_description`
- `urgency`
- `requester_email`
- `troubleshooting_attempted`

Issue category is constrained to:

- Synchronization
- Offline Access
- Schedule
- Application Error
- Other

Urgency is constrained to:

- Low
- Medium
- High

Using predefined values keeps the data consistent and prevents arbitrary AI-generated labels from being stored in Dataverse.

## Human Confirmation

Creating a support ticket changes persistent system state because a new Dataverse record is created.

The tool therefore requires explicit user confirmation before execution.

The agent can prepare the ticket information, but the write operation does not occur until the user approves it.

This provides a guardrail beyond prompt instructions alone.

## Missing Input Handling

Required information should not be silently invented or defaulted.

For example, if urgency is not available from the conversation, the agent asks the user to select Low, Medium, or High before ticket creation.

During testing, default branches in the flow initially caused missing values to be silently assigned. Those defaults were removed so required information must be explicitly available before the flow runs.

## Requester Identity

When available, the agent can use the authenticated user's email as the requester email rather than requiring the user to enter it again.

This reduces unnecessary user input and avoids manual entry errors.

## Structured Data Design

Issue Category, Urgency, and Ticket Status use Dataverse Choice columns rather than unrestricted text.

For example, the system stores:

`Synchronization`

rather than allowing inconsistent values such as:

- Sync
- Sync Problem
- Offline Documentation Sync
- Synchronization Issue

The agent is instructed to use only the approved labels, and the flow maps those labels to their corresponding Dataverse Choice values.

## Sensitive Data Boundary

The support agent is instructed not to include PHI in support tickets.

During evaluation, a synthetic request containing a patient name and date of birth was transformed into a generalized technical description before the ticket was created.

This demonstrates that the agent can preserve the operational problem while excluding unnecessary sensitive information.

## Duplicate Protection

The agent tracks whether a ticket for the same issue has already been created during the current conversation.

If the user asks to create the same ticket again, the agent avoids creating an unintended duplicate.

This protection currently applies only within the conversation and is not a production-grade duplicate detection system.

## Known Limitations

This project is a portfolio prototype using synthetic data.