# Customer Support Ticket & Escalation Management System

## Project Overview

Develop a Salesforce application that enables customers and support representatives to create and manage support tickets. The application will help support teams track customer issues, assign tickets, manage escalations, and monitor resolution through closure.

## Business Requirements

Done 1. Build a Salesforce application for customer support ticket management. 
Done 2. Maintain customer information and support ticket details.
Done 3. Allow support representatives to create tickets with an issue category, description, and priority.
4. Automatically assign tickets to support agents based on issue category or priority.
Done 5. Validate ticket records to ensure required information is provided.
Done 6. Allow agents to update ticket statuses and record resolution details.
7. Automatically escalate high-priority tickets and tickets that remain unresolved beyond a defined period.
8. Require an approval process before escalated tickets can be closed.
Done 9. Publish ticket status and escalation changes as platform events and maintain an escalation/status history.
10. Use asynchronous processing to create follow-up tasks or send notifications for unresolved tickets.
11. Provide search to locate tickets by customer details, ticket number, or issue description.
12. Apply role-appropriate access for support agents, team leads, and administrators.
13. Provide an Agentforce assistant so support representatives can retrieve ticket information and check ticket status.
14. Use generative AI to summarize customer issues and suggest possible resolutions.

## Proposed Salesforce Data Model

### User (Support Agent)

Use Salesforce `User` records for support representatives and team leads. Relevant information includes:

- Name
- Email
- Phone
- Active status

### Contact (Customer)

Use Salesforce `Contact` records to maintain customer information:

- First name
- Last name
- Email
- Phone
- Department

### Case (Support Ticket)

Use Salesforce `Case` as the ticket record. The Case Number serves as the ticket number.

| Field | Purpose |
| --- | --- |
| Case Number | Auto-generated ticket number |
| Contact | Customer who reported the issue |
| Subject | Short issue title |
| Description | Detailed description of the issue; required |
| Type | Issue category |
| Priority | Ticket priority, such as Low, Medium, or High |
| Status | Current ticket status |
| Owner | Assigned support agent or queue |
| Escalated | Indicates whether the ticket has been escalated |
| Created Date | Ticket creation date |
| Closed Date | Ticket closure date |
| Resolution Details | Description of how the issue was resolved |
| Resolved At | Date and time the ticket was resolved |
| Escalation Due At | Deadline used to determine whether the ticket is overdue |
| Escalated At | Date and time the ticket was escalated |
| Escalation Reason | Reason for escalation |
| Closure Approval Status | Approval state for closing an escalated ticket |

### Ticket Status and Escalation History

Publish platform events when a ticket's status or escalation state changes. Maintain a history associated with the ticket containing:

- Case (ticket) reference
- Previous status
- New status
- Change date
- Escalated state

### Follow-up Work

Create follow-up Salesforce Tasks or send notifications for unresolved tickets through asynchronous processing.

## Automation and AI

- Assign tickets automatically using issue category and/or priority.
- Escalate tickets that meet the high-priority or overdue criteria.
- Submit escalated tickets to an approval process before closure.
- Run follow-up task creation or notifications asynchronously for unresolved tickets.
- Let the Agentforce assistant retrieve ticket details and status for support representatives.
- Generate issue summaries and suggested resolutions with Salesforce generative AI capabilities.

## Security

Configure access so that support agents, team leads, and administrators receive permissions appropriate to their responsibilities. Protect customer and ticket information using Salesforce record access, object permissions, and field-level security.

## Decisions to Finalize

- Supported issue categories and priority values.
- Ticket assignment rules for each category and priority.
- Escalation thresholds, including the unresolved-time limit.
- Ticket status values and permitted status transitions.
- Approval routing for escalated ticket closure.
- Follow-up timing, notification channels, and recipients.
- Agentforce actions and the ticket data available to the assistant.
- Generative AI prompt, output review, and handling of suggested resolutions.



## Done

- Create flow for create ticket, getting input from screen flow and create record
- Record-Triggered Flow from case escalated, to trigger the isEscalated field in ticket history
- Record-Triggered Flow when status or eslacation status is changed in ticket -> create a records in ticket history.