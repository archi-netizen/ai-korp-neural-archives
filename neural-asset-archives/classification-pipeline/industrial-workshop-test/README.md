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
