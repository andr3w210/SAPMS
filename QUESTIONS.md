# Decisions needed before implementation

Stage 1 records these uncertainties so the schema can be approved before code or migrations are created. Please answer those you know; unresolved items can remain explicit assumptions for a later decision.

1. **Consumables:** Should consumable supplies and serialized PPE share the `assets` table, use a separate inventory/stock ledger, or should Stage 2 support only individually tracked property? If supplies are needed, what are the unit, stock location, reorder, issue/return, and adjustment requirements? 
2. **Receiving flow:** How are purchase/donation authorization, supplier delivery, inspection, and asset registration connected? Can deliveries be partial, and can one acquisition have multiple receipts? Should an asset receive its property number on acceptance or at a later registration step?
3. **Donations:** Which donor details, acceptance approval, donation valuation, and supporting documents are required? Should donation value be required when unknown?
4. **Asset granularity:** Are identical units always separately property-tagged, or are some tracked only by quantity? Which categories require serial numbers, photos, or a QR tag?
5. **Valuation:** Is `acquisition_cost` always quantity × unit cost, or may freight, discounts, donated appraisal, or adjustments make it differ? What rounding and currency rules apply? Are zero/unknown costs allowed, and may acquisition date be unknown for legacy records?
6. **Property numbering:** What format, prefix, campus/year component, reset policy, and uniqueness scope should property numbers use? Are existing numbers to be imported unchanged?
7. **QR tags:** What tag format should be encoded (opaque ID, property number, or URL)? Must QR tags be unique, immutable, and regenerated/replaced under an audited process?
8. **Approval policy:** What are the exact request, review, approval, dispatch, and receipt steps for transfers? Who may initiate, approve, and confirm receipt? Is separation of requester and approver required, and are thresholds/campus-specific approvers needed?
9. **Disposal policy:** Which disposal types and evidence are needed? Who inspects, recommends, approves, and confirms completion? Does the Campus Administrator approval suffice, or are committee/agency approvals required? How are proceeds and partial disposal recorded?
10. **Accountability:** Can one asset have multiple custodians, employees, or offices concurrently? Is an employee required for an issuance? What acknowledgment statuses and forms are required, and who signs them?
11. **Locations and GPS:** What location hierarchy/codes are standard? Is GPS optional for all locations, and who may view or change coordinates?
12. **Condition/status vocabularies:** Confirm acceptable condition choices and whether they match official government forms. Which statuses should appear for lost, under repair, transferred, unserviceable, and disposed assets?
13. **RPCPPE:** Confirm the required reporting fields, grouping and valuation rules, reporting date/cadence, signatories, output format, and whether the generated file itself must be retained as the official snapshot.
14. **Print forms:** Which exact official form versions/templates and signatures are required for property cards, ICS, PAR, and RPCPPE? Do forms require configurable numbering, campus seals, or approval dates?
15. **Role scope:** Should Campus Administrator approvals apply to all campuses or only assigned campus? Should it view/export personal accountability data? Should Supply Officer be allowed to administer users/roles (currently excluded with Settings)?
16. **Account lifecycle:** Is user access linked to employee records? What happens when an employee separates or transfers offices, and who may deactivate accounts and reference rows?
17. **Legacy imports:** Which tables/entities will be imported, what constitutes a stable legacy key, and which unresolved old references require snapshots? Should duplicates with missing property numbers be imported into a quarantine/reconciliation state?
18. **Audit retention:** How long must audit records and uploaded photos/documents be retained? Should exports and login events include IP address, and are there privacy constraints for before/after snapshots?
19. **Soft deletion and archival:** Confirm that standard policy is deactivate/archive only; under what narrowly defined circumstances may a record be anonymized or purged, and how should its audit reference appear?
20. **Deployment settings:** Confirm target timezone, currency (proposal assumes PHP/MySQL values use a single institution-configured currency), fiscal-year boundary, and whether session/cache/queue database tables will be the standard Laravel tables.

No database name was inspected or used in Stage 1. Before a later migration stage, first run `artisan db:show` and verify that the active database is exactly `sapmsdb`; never use `spamsdb` or `spamsdb_dev`. Do not edit `.env`; any required connection change must be reported as exact lines for the user to apply.
