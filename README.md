# Customer Support Ticket Priority Prediction and Automated Assignment System Using Agentforce

## Project Overview

This project implements a Customer Support Ticket Priority Prediction and Automated Assignment System using Salesforce Agentforce.

The system analyzes customer support ticket information and assigns:
- Predicted Priority
- Priority Score
- Assigned Support Team

The project is implemented using Salesforce Developer Edition, Flow Builder, and Agentforce Builder.

## Team Details

- Team ID: SWTID-2026-8294
- Team Size: 4
- Team Leader: Muthukumar K
- Team Member: Manoj L
- Team Member: Prajin Oaswald A
- Team Member: Kamalesh P

## Technologies Used

- Salesforce Developer Edition
- Salesforce Flow Builder
- Record-Triggered Flow
- Autolaunched Flow
- Agentforce Builder
- Agentforce Employee Agent
- Salesforce Custom Object

## Project Implementation

A custom Salesforce object named `support_ticket__c` is used to store customer support ticket information.

The system uses a Record-Triggered Flow called `set priority` to determine the ticket priority and assign the appropriate support team.

### Priority Rules

- Critical: Urgent issues such as payment failed, crash, or system down
- High: Premium customers and Billing/Refund categories
- Medium: Technical Issue and Account Access categories
- Low: Other/general requests

### Priority Scores

- Critical - 90
- High - 70
- Medium - 50
- Low - 20

### Support Team Assignment

- Billing / Refund → Billing Support
- Account Access → Account Support
- Other categories → Technical Support

## Agentforce Integration

An Agentforce Employee Agent named `Ticket Triage Agent` is used for ticket triage.

A subagent named `Support Ticket Priority Analysis` invokes the Salesforce Flow:

`Support Ticket Priority Flow`

The Flow analyzes the ticket information and returns the ticket record ID, priority level, and final message.

## Testing

The project was tested using different customer support ticket scenarios including:

- Payment failure and refund requests
- Application crash during checkout
- Profile-related questions
- Urgent support descriptions
- Account not found scenarios
- Agentforce ticket-priority queries

The test cases and expected results are documented in the project report.

## Project Report

The complete project report is available in this repository.

## Note

This project is implemented as a rule-based, no-code Salesforce configuration using Flow Builder and Agentforce. It is not a machine-learning model.

## Team

St. Joseph's College of Engineering and Technology

Skill Wallet / TN Skill Project
