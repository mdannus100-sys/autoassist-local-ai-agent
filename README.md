# AutoAssist — AI booking assistant for local businesses

AutoAssist answers the calls a small business misses. When a call goes unanswered it texts the caller back, answers common questions, qualifies the enquiry and books it straight into the business calendar.

> **Status:** in development. Workflows and setup notes are being moved into this repository.

## The problem

Small businesses lose bookings to calls nobody can pick up — during service, after closing, or when one person is running the floor. Those callers rarely ring back. Recovering even a fraction of them pays for the system many times over.

## How it works

1. Twilio receives the missed call and fires a webhook.
2. An n8n workflow opens an SMS conversation with the caller.
3. An LLM handles the exchange: answers FAQs, collects date, time and party size, then confirms.
4. The booking is written to Google Calendar and logged to Google Sheets.
5. A scheduled workflow reports how many bookings were captured outside staffed hours.

## Stack

| Layer | Tool |
| --- | --- |
| Orchestration | n8n |
| Telephony and SMS | Twilio |
| Conversation | LLM API |
| Bookings | Google Calendar API |
| Logging and reporting | Google Sheets API |

## Design notes

- Every conversation ends in one of three states: booked, handed to a human, or closed.
- Nothing is confirmed to the caller until the calendar write succeeds.
- All messages are logged so the business owner can audit what the assistant said.

## Roadmap

- [ ] Publish the four core n8n workflows (intake, conversation, follow-up, daily report)
- [ ] Configuration template for onboarding a new business
- [ ] Pilot results: bookings captured outside staffed hours over 30 days
- [ ] Handover documentation for non-technical operators
