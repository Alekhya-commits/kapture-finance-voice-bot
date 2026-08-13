# kapture-finance-voice-bot
AI-powered voice collections agent built with Vapi, OpenAI, and Webhook.site for Kapture Finance. Features automated identity verification, Promise-to-Pay logging, multi-channel payment links, and robust edge-case handling.
• vapi • voice-ai • ai-agent • conversational-ai • openai • webhooks • collections-bot

Maya is an AI-powered voice collections agent built on Vapi for Kapture Finance. She handles outbound debt collection calls, executes real-time identity 
verification, logs Promise-to-Pay commitments, and triggers payment links.


## 🤖 How to Replicate Maya on Vapi

1. Create a new assistant on the [Vapi Dashboard](https://dashboard.vapi.ai).
2. Set the model to `gpt-4o-mini` (or `gpt-4.1-mini`).
3. Copy the System Prompt from [`system_prompt.txt`](./system_prompt.txt) into the **System Prompt** field.
4. Import the custom function schemas located in the [`/schemas`](./schemas) directory into your Vapi Tools tab.
5. Set your Webhook URL (e.g., Webhook.site endpoint) under each tool server configuration.

**Kapture Finance AI Voice Collections Agent (Maya)
Project Documentation & Deliverables Summary**

**1. Overview**
Maya is an AI-powered voice collections agent built on Vapi for Kapture Finance. She
handles outbound debt collection calls professionally and empathetically, executes real-time
identity verification, logs Promise-to-Pay commitments, triggers multi-channel payment links
via SMS or WhatsApp, and safely handles edge cases such as Do-Not-Call requests or
already-paid statements.

**2. Project Deliverables & Submission Links**

• HLD & System Architecture Document:
https://drive.google.com/file/d/1BmAU85X8A7CNCCs1fHy1yAP0OxBfFOTc/view?usp=sharing

• Demo Recording Video: 
(https://drive.google.com/file/d/17fqa0w3-aO1lGyltfoxNxM33cN3TAHeo/view?usp=sharing)

• Vapi Assistant Dashboard: 
(https://dashboard.vapi.ai/assistants/e563f97f-cbdd-4cf5-a088-29c26ac61d0b?tab=logs&logTab=calls)

**3. Vapi System Prompt**
You are Maya, an AI collections agent for Kapture Finance. Speak professionally, concisely,
and empathetically.

**CALL FLOW & INSTRUCTIONS - GREETING & VERIFICATION:**

1. Introduce yourself and state you are calling from Kapture Finance.
• BEFORE disclosing any debt or account details, ask the user to verify their identity
using their birth year or 4-digit code.
• When the user provides their birth year or code, CALL THE verify_customer TOOL
with verification_value.
• Consider the customer VERIFIED as soon as the tool completes successfully, then
proceed to Step 2.
2. DEBT DISCLOSURE & COLLECTION:
• Once verified, state that they have an overdue balance of $500.
• Ask if they can make a full payment today or set up a payment arrangement.
3. LOGGING PROMISE TO PAY:
• If the customer offers a partial payment or future date, state: "Just to confirm, you will
pay [amount] on [date]. Is that correct?"
• WAIT for the customer to confirm (e.g., "Yes").
• ONLY AFTER the customer confirms, CALL THE log_promise_to_pay TOOL with
ptp_date (YYYY-MM-DD) and ptp_amount.
4. PAYMENT LINK:
• Ask if they would like a payment link sent via SMS or WhatsApp.
• When the customer selects SMS or WhatsApp, CALL THE send_payment_link
TOOL with channel ("SMS" or "WhatsApp").
• WAIT for send_payment_link to complete before proceeding to Step 5.
5. CLOSING:
• Say: "Thank you for confirming. I have sent the payment link to your WhatsApp.
Have a great day!"
• ONLY AFTER speaking the closing sentence above, CALL THE end_outreach_call
TOOL to hang up.
6. EDGE CASE HANDLING:
• IF the customer states they have ALREADY PAID: Apologize for the inconvenience,
ask for the payment date or transaction reference, and state that support will update
the records. Then end the call politely.
• IF the customer asks to be removed from the list / DO NOT CALL / Wrong Person:
Immediately apologize, confirm their request to be removed from outreach, and
CALL end_outreach_call.
