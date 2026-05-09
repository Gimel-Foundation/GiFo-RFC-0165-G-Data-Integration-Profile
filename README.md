# GiFo-RFC-0165 (V0.7 - Working Draft – Under Review)

G-Data Integration Profile - Combined Credential- and Platform-bound Enforcement (CCPE-H)

New Request for Comments of Gimel Foundation (GiFo RFC) - Establishung G-Data Integration Profile - Combined Credential- and Platform-bound Enforcement (CCPE-H)

Abstract of RFC: CCPE-H (G-Data) is the data-authorisation profile of the GAuth framework. It lets an autonomous agent read, derive from, transform, and emit data assets on a principal's behalf under a signed delegation credential, while the data platform's own access-governance still applies.
The profile defines:
•	a Data-Mandate envelope (§3.1) — a Power-of-Attorney credential per RFC 0115 specialised for data;
•	a purpose-bound decision surface — purpose → dataset-scope → operation — with purpose-fit as a pre-action invariant and behavioural-conformance as an in-action / post-action invariant;
•	a bipolar enforcement chain — Power-PEP (credential-bound, Phase 1) followed by Data-PDP (platform-bound, Phase 2), reconciled by more-restrictive-wins;
•	engine-neutral cookbook bodies for nine data-platform substrates across three families: enterprise data-governance catalogues (Collibra, Atlan, Informatica, IBM watsonx.data / Cloud Pak for Data, Microsoft Purview); access-governance overlays (Immuta as canonical, Privacera as alternative); platform-native catalogues (Databricks Unity Catalog, Snowflake Horizon, AWS Lake Formation / Glue Data Catalog);
•	the CCPE-H-NCI / NCP / NCO non-conformant-variant taxonomy (§4.6);
•	the S1 / S2 / S3 deployment-scenario architecture (§2.6) where only S2 is conformant to G-Data;
•	the §13.A GAuth Open-Core Reference Connector Slot Registry foundation, naming the multi-instance `data_pdp` slot (Type-A) and the single-instance `data_authority` slot (Type-B), the tariff-tier matrix, and the open-core symmetry rules;
•	the §6.5a per-call metering rules for `recordDataDecision()` and `recordLineageAttestation()`;
•	the §15 IANA-style reservations for tariff-tier / slot-type / `phase2_evaluation.profile` values; and
•	Appendix A - the formal NIST AI RMF v1.0 MAP-function cross-walk against the CCPE-H normative surface.

How CCPE-H Works in 60 Seconds (Informative)
A worked example: a market-research agent prepares a quarterly customer-segment summary on behalf of its principal at data platform acme-warehouse.
   [principal]
       │ issues
       ▼
  [Authority]──────────► data-mandate
                            purpose=customer-segmentation,
                            dataset-scope=acme.warehouse.customers.*
                                         minus PII columns,
                            operations={read, aggregate, derive},
                            no-egress-outside-tenant,
                            8h, no-retraining
       │
       │  agent issues SELECT … aggregating customer features
       ▼
  [Data-PEP] ── Phase 1 (RFC 0117 16-check + purpose-fit) ── permit
       │
       │ (only on permit/constrain)
       ▼
  [Data-PDP @ acme-warehouse] ── Phase 2 (catalogue policy + row/column ACLs) ── permit
       │
       ▼
  reconciled verdict = permit  ──►  query proceeds; lineage attested
   audit:    data.action_decided + data.platform_bound.decided
             + data.purpose_attested + data.lineage_recorded
Three things that make this profile distinct from a "the warehouse already has row-level security" flow:

•	Purpose-bound mandate. The mandate names the purpose under which the agent is delegated, not just the dataset. A query that is row/column-permitted by the platform but purpose-misfit (e.g. an aggregation mandate used to extract per-row PII) is denied at Phase 1 even where Phase 2 would permit.

•	Two-stage enforcement. The Power-PEP enforces what the principal delegated (purpose, scope, operations, retention, retraining-prohibition, egress-boundary); the Data-PDP enforces what the platform allows (row/column ACLs, masking policies, dataset classification). The stricter of the two wins. A Phase-1 deny short-circuits Phase 2.

•	Lineage attestation as in-action evidence. Every permitted action emits a data.lineage_recorded audit event binding the action's input-dataset references, the operation class, and the output-artefact reference into the trace. Behavioural conformance is then auditable post-hoc: a downstream reviewer can verify that the derived artefact's content stays inside the purpose envelope.

If the Data-PDP doesn't answer within phase2_timeout_ms, the mandate's fail_disposition decides: fail_closed denies; fail_drop_egress_only denies egress-class operations but lets read-only / in-platform operations through if Phase 1 already permitted.



You are more than welcome to contribute !

Legal Provisions for users of this page

Please see the Legal Provisions under https://gimelfoundation.com

In particular the following terms apply:

GiFo RFC 0080 Legal Provisions for the Gimel Foundation

GiFo RFC 0090 Legal Provisions Related to Gimel Foundation Documents

GiFo RCC 0100 Rights Contributors Provide to the Gimel Foundation
