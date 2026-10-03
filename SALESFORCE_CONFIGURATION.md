# Salesforce Configuration

This file records the implementation described in the project report.

## 1. Custom object

- Label: `support ticket intelligence`
- API name: `support_ticket__c`
- Record Name: `Ticket Number`
- Data type: Auto Number
- Display format: `TKT-{0000}`
- Starting number: `1`

## 2. Fields

| Label | API name | Type | Values / description |
|---|---|---|---|
| ticket number | `Name` | Auto Number | `TKT-{0000}` |
| subject | `subject__c` | Text (255) | Required |
| describtion | `describtion__c` | Long Text Area (32000) | Required |
| category | `category__c` | Picklist | Billing, Technical Issue, Account Access, Product Inquiry, Refund, Other |
| custumer type | `custumer_type__c` | Picklist | Free, Paid, Premium |
| channel | `channel__c` | Picklist | Email, Phone, Chat, Social Media |
| stitus | `stitus__c` | Picklist | Open, In Progress, Resolved, Closed |
| priority | `priority__c` | Picklist | Low, Medium, High, Critical |
| predict priority | `predict_priority__c` | Picklist | Low, Medium, High, Critical |
| priority score | `priority_score__c` | Number (3,0) | Filled by Flow |
| assigned team | `assigned_team__c` | Text (100) | Filled by Flow |
| customer | `customer__c` | Lookup (Account) | Account the ticket belongs to |

> The API names above preserve the spelling used in the report, including `describtion`, `custumer`, and `stitus`.

## 3. Record-triggered Flow: `set priority`

- Object: `support ticket intelligence`
- Trigger: record is created
- Optimization: Fast Field Updates
- Assignment element label: `Set Values`

Assignments:

- `{$Record.predict_priority__c}` = `PriorityF`
- `{$Record.priority_score__c}` = `ScoreF`
- `{$Record.assigned_team__c}` = `TeamF`

## 4. Autolaunched Flow: `Support Ticket Priority Flow`

Input:

- `AccountNameInput` — Text

Outputs:

- `RecordID` — Text
- `PriorityLevel` — Text
- `FinalMessage` — Text

Flow structure:

`Start → Get Account → Get Ticket → Decision (Analyze Description) → Assignment → End`

`GetAccount`:
- Object: Account
- Condition: Name equals `AccountNameInput`
- Store first record

`GetTicket`:
- Object: support ticket intelligence
- Condition: customer equals `GetAccount.Id`
- Store first record

Decision:
- High Priority: description contains `urgent`, `not working`, or `failure`
- Medium Priority: description contains `slow` or `delay`
- Default: Low Priority

## 5. Agentforce

Agent:
- `Ticket Triage Agent` — Employee Agent

Subagent:
- Name: `Support Ticket Priority Analysis`
- API name: `Support_Ticket_Priority_Analysis`

Subagent scope:
- Analyze support ticket descriptions and determine High, Medium or Low priority.

Agent action:
- Reference action type: Flow
- Reference action: `Support Ticket Priority Flow`
- Input: `AccountNameInput`
- Outputs: `RecordID`, `PriorityLevel`, `FinalMessage`
- Loading text: `Checking your ticket priority...`

The report also records an additional numeric `accountid` input whose logic is not used and whose description tells the agent not to ask the user for it.
