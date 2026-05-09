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



You are more than welcome to contribute !

Legal Provisions for users of this page

Please see the Legal Provisions under https://gimelfoundation.com

In particular the following terms apply:

GiFo RFC 0080 Legal Provisions for the Gimel Foundation

GiFo RFC 0090 Legal Provisions Related to Gimel Foundation Documents

GiFo RCC 0100 Rights Contributors Provide to the Gimel Foundation
