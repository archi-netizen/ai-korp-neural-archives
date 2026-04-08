# AI-KORP | Neural Asset Archives
**Applied Research: Investigating automated design taxonomies using AWS cloud infrastructure for AEC and Branding.**

## 1. Executive Summary
This repository serves as a technical log for a proof-of-concept study. The objective is to evaluate how cloud-native AI services can transition static architectural and branding archives into "Active Knowledge Bases."

By utilizing a serverless pipeline, we move from manual filing to a system that "understands" architectural intent, material composition, and brand application.

## 2. Theoretical Framework: The AI-KORP Baskets
This study operationalizes the **AI-KORP Framework**, specifically focusing on the **Intellectual (Knowledge)** and **Spatial (Context)** baskets. 

- **Input:** Raw design assets (Renders, Brand Mockups, Site Photos).
- **Process:** AWS-driven extraction of visual and contextual metadata.
- **Output:** A searchable, tagged ecosystem for design synthesis.

## 3. The Technical Stack (AWS)
To ensure professional data sovereignty, the pipeline is built on a modular, private cloud environment:

| Service | Role |
| :--- | :--- |
| **Amazon S3** | Object storage for high-resolution design assets. |
| **AWS Lambda** | Event-driven logic to trigger analysis on upload. |
| **Amazon Rekognition** | Computer vision for label detection (Materials, Objects, Styles). |
| **Amazon Bedrock** | LLM reasoning to synthesize raw tags into design summaries. |

## 4. Visual Study & Analysis
Below are the sample inputs used to test the pipeline's granularity:

### Asset A: Brand Archetype
*Testing text detection and graphic consistency.*
![Brand Toolkit](./Asset_1_Branding.jpg)

### Asset B: Spatial Context (Industrial Workshop)
*Testing complex environment recognition (Gantries, Concrete, Workflow).*
![Workshop Render](./Asset_2_Spatial.jpg)

## 5. Compliance & Governance
This research is conducted with a "Security-First" mindset:
- **Data Privacy:** All processing occurs within a private VPC.
- **Ethics:** Aligned with the **EU AI Act** regarding transparent data processing and human-in-the-loop verification.

### 🔍 Live Audit: Machine Perception
I analyzed the primary workshop render using **Amazon Rekognition** to extract a spatial taxonomy.

**Top High-Confidence Labels:**
* **Architecture:** 99.9%
* **Factory / Industrial Building:** 99.9%
* **Person:** 98.6% (Validating human scale)
* **Manufacturing:** 72.8%

**Raw Data Archive:**
Download the verified architectural taxonomy: [Master Label List (JSON)](./Asset_2_Rekognition_Raw.json)

---
*Note: This is a non-commercial research project exploring workflow optimization for the AEC and Brand Design sectors.*

---

## System Architecture
To ensure professional-grade security, the pipeline is built on a modular AWS environment. This "sandboxed" approach ensures that design assets remain private and are excluded from public AI training loops.

```mermaid
graph TD
    %% Ingestion Layer
    A[Design Asset: Render/Photo] -->|Upload| B(Amazon S3: Research-Archive)
    
    %% Logic Layer
    B -->|S3 Event Trigger| C{AWS Lambda: Boto3 Script}
    
    %% Analysis Layer
    C -->|Analyze Image| D[Amazon Rekognition: Vision Engine]
    D -->|Extract Labels| C
    
    %% Reasoning Layer
    C -->|Synthesize Context| E[Amazon Bedrock: Claude 3.5]
    E -->|Generate Design Summary| C
    
    %% Output Layer
    C -->|Final Metadata| F[(Neural Archive Database)]
    F --> G{Creative Basket}
    F --> H{Spatial Basket}
    F --> I{Intellectual Basket}

    %% AWS Branding Colors
    style B fill:#FF9900,stroke:#232F3E,color:#fff
    style C fill:#FF9900,stroke:#232F3E,color:#fff
    style D fill:#3F8624,stroke:#232F3E,color:#fff
    style E fill:#D05C45,stroke:#232F3E,color:#fff
