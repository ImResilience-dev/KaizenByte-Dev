# Quant Terminal with the IMIT OVR Playbook

A one-paste install prompt for the free, open source [Quant Terminal](https://part-timequant.com) app (MIT licence, by Lewis Jackson), with an IMIT OVR framework banner and Playbook window from the OVRstanding Group.

## How to use it
1. Open Claude (or any coding agent that can run commands on your computer).
2. Paste the contents of [`install-prompt.txt`](install-prompt.txt) and send it.
3. Answer the two short questions (what you trade, which symbols). It installs, tests, and opens the terminal in your browser.

Needs Node.js 18 or newer. No accounts, no API keys.

## What the OVR banner adds
- A top banner with the loop: Edge, Control, Acceptance, Delivery, Exhaustion, Reset, and the four-layer reading order.
- A **Playbook** button with the setups (B1 to N2), tier sizing, trade management, all 19 states, the five sequences, how control shifts, and operator discipline.

[`ovr-banner.js`](ovr-banner.js) is the small script that installs it. It is safe to run again, and it updates in place:

```
cd quant-terminal
node ovr-banner.js
```

## Credit and licence
Quant Terminal is copyright Lewis Jackson and released under the MIT licence. The patch only changes the top banner and adds a Playbook window, and leaves the app's LICENSE and NOTICE files in place. This project is not affiliated with or endorsed by the app's author or by TradingView, Inc.

Educational only. Nothing here is financial advice.
