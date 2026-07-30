# Neural Asset Archives

This folder documents the core proof-of-concept pipeline of the AI-KORP 
research: the conversion of static architectural and branding assets into 
an active, queryable knowledge base using AWS cloud infrastructure.

The Neural Asset Archives is the applied technical layer of the AI-KORP 
framework. It tests whether cloud-native AI services can extract meaningful 
design intelligence from raw visual assets — renders, brand mockups, site 
photographs — and return structured, searchable metadata that supports 
design synthesis and governance decisions.

**Status note:** the three assets below were classified individually through 
the Amazon Rekognition console (Label Detection tool). The S3 → Lambda → 
Bedrock stages shown in the architecture diagram represent the intended 
automated pipeline; the Bedrock synthesis step has not yet been run against 
these assets, and this README does not claim otherwise.

---

## What This Is

A classification workflow tested against AWS Rekognition, returning:

- **Visual labels** — objects, materials, spatial typologies, architectural 
  elements identified by machine vision
- **Confidence scores** — numerical weighting of each label, used to 
  evaluate classifier reliability and ripeness
- **Governance flags** — where classification confidence, data provenance, 
  or disclosure conditions are insufficient to treat output as design authority

Planned but not yet executed against these assets:

- **Design summaries** — LLM-synthesised narratives (Amazon Bedrock) 
  contextualising raw label output within architectural and brand design 
  language
- **Automated ingestion** — S3 upload trigger and Lambda orchestration, 
  as shown in the architecture diagram below

This pipeline operationalises the **Ripeness axis** of the AI-KORP framework:

| Ripeness Level | Symbol | Condition |
| :--- | :---: | :--- |
| Sourcing | ○ | Asset ingested, not yet classified |
| Sorting | ◐ | Classification complete, human review pending |
| Stored | ● | Verified, disclosed, cleared for design use |

No asset moves from Sorting to Stored without human-in-the-loop review.

---

## Pipeline Architecture (proposed)

```mermaid
graph TD
    A[Design Asset: Render / Photo / Site Image] -->|Upload| B(Amazon S3: Research-Archive)
    B -->|S3 Event Trigger| C{AWS Lambda: Boto3 Script}
    C -->|Analyze Image| D[Amazon Rekognition: Vision Engine]
    D -->|Extract Labels + Confidence Scores| C
    C -->|Synthesize Context| E[Amazon Bedrock: Claude 3.5]
    E -->|Generate Design Summary| C
    C -->|Final Metadata + Governance Flag| F[(Neural Archive Database)]
    F --> G{Creative Basket}
    F --> H{Spatial Basket}
    F --> I{Intellectual Basket}

    style B fill:#FF9900,stroke:#232F3E,color:#fff
    style C fill:#FF9900,stroke:#232F3E,color:#fff
    style D fill:#3F8624,stroke:#232F3E,color:#fff
    style E fill:#D05C45,stroke:#232F3E,color:#fff
```

This diagram shows the pipeline's intended end-to-end architecture. The 
Rekognition stage (D) has been executed manually via the console for the 
three assets documented below; S3 ingestion, Lambda orchestration, and 
Bedrock synthesis (B, C, E) have not yet been run.

---

## Folder Structure

neural-asset-archives/
├── README.md
└── classification-pipeline/
└── industrial-workshop-test/
├── README.md
├── Asset_1_Branding.jpg
├── Asset_2_Rekognition_Raw.json
├── Asset_2_Spatial.jpg
├── Asset_3_Material.jpg
├── metadata_sample.json
└── results/

---

## Assets Tested

### Asset A: Brand Archetype
**File:** `Asset_1_Branding.jpg`
**Basket:** Creative
**Test objective:** Text detection, graphic consistency, brand mark recognition.
**Ripeness outcome:** Sorting ◐ — classifier identifies graphic and typographic 
elements but cannot verify data provenance or licensing status of training 
corpus. Human review required before design use.

**Rekognition labels:**

| Label | Confidence |
| :--- | :--- |
| Diagram | 90.6% |
| Business Card | 82.8% |
| Paper | 82.8% |
| Text | 82.8% |
| Chart | 56.4% |
| Plan | 56.4% |

---

### Asset B: Spatial Context — Industrial Workshop
**File:** `Asset_2_Spatial.jpg`
**Basket:** Spatial + Intellectual
**Test objective:** Complex environment recognition — gantries, concrete, 
workflow, human scale.
**Ripeness outcome:** Stored ● — high-confidence classification across 
architectural, industrial, and human-scale labels. Results verified and 
disclosed. See classification-pipeline/industrial-workshop-test/ for full 
methodology and raw JSON output.

**Rekognition labels:**

| Label | Confidence |
| :--- | :--- |
| Architecture | 99.8% |
| Building | 99.8% |
| Factory | 99.8% |
| Person | 98.6% |
| Floor | 95.3% |
| Flooring | 80.6% |
| Indoors | 73.7% |
| Manufacturing | 64.9% |

---

### Asset C: Material Context
**File:** `Asset_3_Material.jpg`
**Basket:** Spatial *(tentative — flagged for confirmation, not yet reviewed against the framework's criteria)*
**Test objective:** Surface and material condition recognition.
**Ripeness outcome:** *(not yet assigned — pending human review)*

**Rekognition labels:**

| Label | Confidence |
| :--- | :--- |
| Corrosion | 89.9% |
| Rust | 89.9% |
| Door | 59.1% |

---

## Key Finding

Brand and architecture are not two separate signal layers in the built 
environment. At building scale, a company's colour, mark, and typographic 
system travel identically from logo to facade to fleet. The classifier 
learns from that fused layer whether or not the learning is governed.

This finding, established at building scale through the Neural Asset Archives 
pipeline, is extended to urban and aerial scale in the Urban-Scale Evidence 
section of this repository.

---

## Governance and Compliance

Rekognition testing was performed through the AWS console under the 
researcher's own account; no assets were submitted to a public AI training 
loop. Research is conducted in alignment with:

- **EU AI Act, Article 4** (applicable since 2 February 2025) — AI literacy: 
  the Ripeness axis operationalises practitioner-level literacy requirements
- **EU AI Act, Article 50** (applicable from 2 August 2026) — Disclosure: 
  classification and generative outputs are flagged with their Ripeness 
  status before design use
- **Data sovereignty:** assets were processed under the researcher's own 
  AWS account and are not submitted to third-party training pipelines

---

## Related Publication

This pipeline is documented as the methods section of:

**Mate, K. (2026). Sorting the Harvest at Scale: A Governance Framework 
for Generative AI, from Brand Systems to Urban Futures. Zenodo. 
https://doi.org/10.5281/zenodo.21460708**

Intended for submission to the Special Issue *Generative Urbanisms: 
Artificial Intelligence and the Design of Urban Futures*, Architectural 
Intelligence (Springer Nature). Submission deadline: 30 November 2026.

---

*Kaushambi Mate · Independent Researcher · 
ORCID: https://orcid.org/0009-0008-5892-3576*
