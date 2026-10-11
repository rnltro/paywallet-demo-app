PayWallet — a payment wallet designed to be broken
A complete, single-file payment wallet that simulates the entire card andP2P lifecycle: Friends & Family vs Goods & Services fees, card declines,insufficient funds, 3D Secure step-up, buy-now-pay-later, savings interest,and fraud holds. One HTML file. No backend. No build step. No real money.

Not affiliated with PayPal or Stripe. PayWallet is an original demoinspired by real payment platforms.

🎯 Try to break it
Open the live demo → Profile → use the demo account → then attempt tomake a payment fail from Add money → Card (Stripe-style):

Test card	What happens
4242 4242 4242 4242	Succeeds (+1% cashback on purchases)
4000 0000 0000 0002	Declined by issuer
4000 0000 0000 9995	Insufficient funds
4000 0027 6000 3184	Triggers 3D Secure (code: 123456)

💡 The idea major wallets haven't shipped
Before you confirm any payment, PayWallet shows F&F and G&S side byside — who pays the fee, what the recipient actually nets. Real walletsshow fees contextually; fee surprise is one of their mostcomplained-about behaviors. This demo takes a position: fees belong onthe confirmation screen, compared, before you commit.

🏗️ How it works — three design decisions
One seam. Every card authorization routes through a singleprocessCard() function. Swap its body for a real Stripe API call andthe card layer goes live. Everything else is agnostic.
One ledger. Card, bank, and balance rails all write to the sametransaction store — exactly how real wallets consolidate rails.
A scripted counterparty. Requests get paid, recipients reply,friends send you money — the two-sided payment loop with zeroinfrastructure.
Every transaction is inspectable: open any payment → "View rawtransaction data" → the mock record as an API would return it.

✨ Features
Payments — F&F / G&S with real fee table · requests with simulatedresponses · paywallet.me-style link & QR · split requests · notes ·delivery receipts & thank-you replies

Card lifecycle — live formatting & brand detection · Luhn validation ·4 behavioral test cards · 3D Secure step-up on risk · save-card &CVC-only express checkout · declines with inline recovery

Money management — Pay in 4 (BNPL with autopay simulation) · Savingspocket with time-based interest accrual · 1% G&S cashback · transfers tobank (standard vs instant fee comparison) · spending insights

Trust & safety — 2-step verification (simulated SMS) · adjustablesecurity-check sensitivity · device management · activity search &filters · raw transaction viewer

🚀 Running it
Option 1 — just open it:Double-click index.html. That's the whole deployment.

Option 2 — localhost (recommended for testing):

# Python (preinstalled on macOS/Linux)python3 -m http.server 8080# then visit http://localhost:8080# Nodenpx serve .# VS Code: install "Live Server" extension → right-click index.html → Open with Live Server
Demo login: demo-user@paywallet.demo / demo1234 (2-step code
appears in the simulated SMS banner), or use the one-tap demo button.

⚠️ What's simulated (all of it)
Balances, people, banks, cards, and every payment are fictional and run
locally in your browser. Fees and rates are modeled on published
real-world rates (2.9% + $0.30 · 3.49% + $0.49 · 1% instant transfer ·
4.30% APY) but nothing is charged. Data persists in localStorage and
never leaves your machine.