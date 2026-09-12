# Solution Architecture

The Northstar Mobile Support Agent combines conversational AI, grounded troubleshooting knowledge, tool orchestration, a deterministic agent flow, and persistent Dataverse storage.

```mermaid
flowchart TD
    U[User] --> A[Northstar Mobile Support Agent]

    A --> K[Northstar Mobile Support Knowledge]
    K --> A

    A --> D{Ticket needed?}

    D -->|No| R[Troubleshooting Response]
    D -->|Yes| I[Collect Structured Inputs]

    I --> C{User Confirms?}

    C -->|No| X[Cancel Ticket Creation]
    C -->|Yes| T[Create Support Ticket Tool]

    T --> F[Create Northstar Support Ticket Flow]

    F --> REF[Generate Ticket Reference]
    REF --> CAT[Map Issue Category]
    CAT --> URG[Map Urgency]
    URG --> DV[Dataverse Connector]

    DV --> DB[(Support Tickets Table)]

    DB --> OUT[Return Ticket Reference]
    OUT --> A
    A --> U
```
