+++
tags = ['Developer Log', 'AI']
title = 'Developer Week 060'
date = 2025-09-10T20:20:07+01:00
draft = false
+++

## Work Log

Fell sick on 8/29 and did not recover. Ended up in the hospital for over 48 hours with "walking pneumonia", and am still actively recovering. (_writing this well after the fact_)

This was a near total loss. Though I did manage to pull out a work day in a brief spell where the fever broke before coming back with vengeance.

### Fri 9/5

- Bug fix: Amazon order numbers not pulling into the JSON
  - Code solution came to me in the middle of a fever dream
- Spent all day fixing bugs as the company had turned off my agents
- Bug fix: Return Agent sending JSON obj, rather than string
- Bug fix: AI agent responding to cancellation requests initiated by the shipping team.
- Bug fix: AI Double Messages due to customers double messaging within the message queue window
- Modify Product Availability to give better windows beyond (2-9 business days)
- Update: Return Agent to handle multi message at the same time
- Create backend API for Awaiting Shipment status
