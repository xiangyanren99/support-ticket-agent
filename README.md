# support-ticket-agent
A Copilot Studio agent that troubleshoots user issues and creates structured support tickets through an automated workflow.

Who is the user?
What problem do they experience?
How do they handle it today?
What will the proposed solution do?
How will success be measured?
What must the solution not do?

Application users often contact support without providing the technical details required to investigate their issue, leading to repeated follow-up questions and delayed resolution. Support employees must manually collect information, search troubleshooting documentation and enter the request into a ticketing system. This project will demonstrate a Copilot Studio agent that guides users through troubleshooting, collects structured issue details and invokes an automated workflow to create a support-ticket record after receiving explicit confirmation. The agent will use synthetic scenarios and will not collect patient-identifying or confidential information. Success will be measured through test cases covering required-field collection, appropriate tool invocation, confirmation behavior, duplicate prevention and graceful integration-failure handling.
