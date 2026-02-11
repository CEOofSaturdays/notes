# Coates Hire Transport Validation Agent Spec (Draft)

## Objective
Build an Agno-based workflow that:
1. Parses Coates Hire invoices (PDFs)
2. Identifies and extracts all transport-related charges
3. Validates transport charges against contract rates/terms + contract variations
4. Groups unsupported/non-validated transport charges by month
5. Generates detailed, legal-style request letters to Coates Hire asking for supporting evidence

## Current business stance
- Transport charges will not be paid unless validated against contract terms and variations.
- For invoices lacking supporting information, produce month-grouped evidence requests.

## Clarifications needed (blocking for final spec)

### 1) Inputs and source of truth
- Where will the documents live?
  - Invoice PDFs path/repo/cloud location?
  - Master contract PDF location?
  - Contract variation docs location?
- Are there multiple contracts/variations or just one active agreement family?
- Do we have any structured export (CSV/ERP dump) alongside PDFs?

### 2) Transport charge identification rules
- What labels should count as transport-related?
  - e.g. "Transport", "Delivery", "Pickup", "Freight", "Cartage", "Mobilisation", "Demobilisation"
- Should the agent use exact keyword matching only, or fuzzy/semantic matching with confidence scores?
- Should negative transport lines (credits/reversals) be included and netted?

### 3) Contract validation logic
- How are transport rates defined in contract docs?
  - Flat fee, distance bands, zone-based rates, equipment-class rates, minimum charges, after-hours multipliers?
- Which variation document overrides apply, and from what effective dates?
- What tolerance is acceptable before flagging (e.g. $0, ±1%, ±$5)?
- Is GST/tax validated separately or excluded from transport comparison?

### 4) Matching invoices to contract terms
- How should invoice lines map to contract rate cards?
  - By site, job number, equipment class, region, branch, or description text?
- What should happen when mapping is ambiguous?
  - Fail closed (mark unsupported) or send to manual review queue?

### 5) Monthly grouping and legal letter output
- Group by:
  - Invoice date month, service date month, or due date month?
- One letter per month overall, or one per month per site/project?
- Preferred tone/jurisdiction style for "legal-like" letters?
  - Firm commercial request vs formal legal notice language?
- Required letter metadata:
  - Addressee name/title/email?
  - Company legal entity details?
  - Reference contract number and variation IDs?
- Delivery channel:
  - PDF letter, Word doc, email draft, or all?

### 6) Evidence request expectations
- What exact evidence is acceptable from Coates?
  - Dockets, run sheets, GPS logs, delivery manifests, timesheets, signed PODs, route calculations?
- Required response deadline language?
  - e.g. "within 7 business days"
- Should letter include consequences/escalation language if evidence not provided?

### 7) Workflow, controls, and audit
- Who approves final letters before sending?
- Should agent only draft, or also send?
- Where should audit outputs be stored?
  - JSON evidence pack + human-readable report location?
- Any redaction/privacy requirements for stored invoice data?

### 8) Success criteria
- What defines a successful v1?
  - % extraction accuracy target?
  - false-positive tolerance?
  - turnaround time per invoice batch?

## Proposed next deliverable
Once answers are provided, produce:
1. Full Agno technical spec
2. Mermaid process diagrams (preferred)
3. Canonical schema for invoices/transport lines/contract rules
4. Rule engine pseudocode + exception taxonomy
5. Letter-generation template set (monthly grouped)
