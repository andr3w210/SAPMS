# SAPMS module build order

This order establishes authorization and durable reference data before transactional workflows. Stage 1 is design only; each module starts only after the user authorizes the next stage.

1. **Foundation and roles** — Laravel/Filament `/admin` panel, standard users with bcrypt, active users and roles, historical user-role assignment, deny-by-default policies, Administrator and Supply Officer full access except the Settings boundary, Campus Administrator read-only access with transfer/disposal approvals and report exports, and Settings restricted to Administrator. Create the other named roles but grant them no panel access. Audit login and privileged actions.
2. **Reference data** — campus, offices, locations, employees and assignments, classifications, account codes, funds, item names, units, brands/models, suppliers, and responsibility codes. Add active/inactive controls, uniqueness, and FK protections.
3. **Employees and offices** — effective-dated employee assignments, office hierarchy, campuses/extensions, transfer-proof retirement rules, and employee links to user accounts only if a later requirement calls for one.
4. **Assets** — property register, purchase/donation acquisitions, identity and QR tagging, condition, valuation validation, photos, and asset-specific location history. Set required-field policy only after open questions are answered. This module stores tracked property; stock supplies require a decision.
5. **Accountability** — issue/custodianship records with office, optional employee, responsibility code, status, acknowledgment form generation, and effective-dated accountability history.
6. **Transfers** — request, item selection, approvals, dispatch/receipt, validation of current custodian/location, transactional history updates, cancellations, and audit trail. Campus Administrator may approve; exact approval chain awaits decision.
7. **Disposals** — request, item eligibility and valuation, approvals, completion details, status change, disposition evidence, and audit trail. Never delete disposed assets.
8. **Distributions and receiving** — receiving records and discrepancies, delivery evidence, distribution/issuance to offices or employees, acknowledgment documents, and quantity-stock workflow if authorized. Confirm relationship among purchase acquisition, receiving, and issuing before implementing.
9. **Inventory counts** — scoped count sessions, QR/serial lookup, expected-versus-observed facts, variances, reconciliation, and permanent count history.
10. **Reports and print forms** — property card, Inventory Custodian Slip, Property Acknowledgment Receipt, RPCPPE snapshot/report export, inventory variance and asset registers. Keep reproducible report snapshots and enforce role export permissions.
11. **Dashboard** — role-scoped counts and summaries for active assets, custody, transfers, disposals, count variances, and pending approvals; links into authorized records only.

Every stage adds append-only audit events, foreign-key-safe archival behavior, and SQLite in-memory tests where tests are requested. No trip ticket module is planned.
