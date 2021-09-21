# Introduction

## Amazon Connect is a powerful contact center solution by AWS. It provides web-based softphone for agents. The default softphone is generic and simple. With Arta, the softphone has been rewritten specific to Freshdesk.
The custom contact control panel (CCP) offers interesting features such as:
- Setting up call logs, customer identification 
- Visibility for agents into caller history, previous ticket info
- Agents enabled to take notes while talking to the customer
Given below is a list of key features available (new features are being added continuously).
On-Call (on receipt of an incoming call)
- Known Caller
  - If a caller is already in the Freshdesk contacts, then the Caller Name will be displayed to the agent.
  - All open tickets for that caller will be displayed to the agents. If there’s more than one open ticket available for that user, then the ticket list will be displayed to the agent.
  - The agent will have an option to create a new ticket if the caller is calling for a new issue.
  - The agent could select any ticket from the list and add notes to that ticket while talking to the caller.
  - If no open tickets are available for a caller, then a new ticket will be created automatically.
- Unknown Caller
  - If a caller is not in the Freshdesk contacts, then the Caller Name will be displayed to the agent as “Unknown Caller”.
  - If the caller is Unknown, then a ticket will not be created automatically. But the agent will have the option to create a ticket if required.
Post Call 
- Show call history specific to agent – last 25 calls.
- Make outbound calls by clicking call history.
- Create contact by selecting a number from the call history.
- Call related information will be added into the respective ticket as comment automatically.
- Ticket updated with Amazon Connect log reference.
Contact Page
- Once contact number is clicked in the contact page it will trigger an outgoing call
Ticket Page
- From the ticket page, the agent can make an outbound call to the caller.
Common Features
- The agent could search for contacts from the dial pad.
- The agent could change their availability status.
- The agent could send call logs to support.  