# Warehouse Project - Full Version (150 points)

## Foundation
- [x] Bring the Stage 1 warehouse classes into the project root.
- [x] Use one coordinator (`StoreSystem`).
- [x] Compile with `javac *.java`; run with `java UserInterface`.
- [x] Keep input/output in the UI and business rules in the model.

## Features
- [x] Create clients and products with unique IDs.
- [x] Manage client wishlists; replace quantities for existing entries.
- [ ] Review wishlist items at checkout; allow quantity changes and extra products.
- [ ] Fill orders from stock; put shortages on each product's FIFO waitlist.
- [ ] Clear processed wishlist entries to prevent duplicate orders.
- [ ] Generate dated invoices for supplied items only; preserve unit prices.
- [ ] Charge client balances and record dated transactions.
- [ ] Record payments separately; allow overpayments to become client credit.
- [ ] Receive shipments: fill waitlists first, invoice and charge each fulfillment,
      retain partially filled requests, then add leftovers to stock.
- [ ] Display clients/balances, products/stock, wishlists, waitlists,
      invoices, transaction histories, outstanding balances and quantities.
- [ ] Validate IDs, quantities and money; use consistent money arithmetic.
- [ ] Preserve data and ID counters when saving/loading (recommended).

## Verification and Submission
- [ ] Run every operation and query in the final assignment through the menu.
- [ ] Check final P1-P5 stock: **92, 7, 25, 33, 39**.
- [ ] Check final balances: **C1 $55 credit; C2 $51 credit; C3 $48 owed;
      C4/C5 $0** (after separate $100 payments for C1 and C2).
- [ ] Check invoices: **C1 $40 + $5; C2 $49; C3 $45 + $3**.
- [ ] Test partial shipments, invalid input, empty lists and repeated checkout.
- [ ] Capture the required terminal test session and expected/actual results.
- [ ] Use a private group repo; invite `rsarnath` and `SajalCodeHub`.
- [ ] Submit the D2L report: Full version, contribution percentages, repo URL,
      test table and unlisted video link; every member speaks in the video.

Source: `Project1FinalImplementation.docx` and the PDFs in `PreviousAssignments`.
