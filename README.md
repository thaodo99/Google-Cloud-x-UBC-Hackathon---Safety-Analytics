# Safety Incident Pattern Mining & AI Safety Assistant
**Google Cloud Hackathon – Methanex Challenge #2**  
**Team 8: Safety in Your Area**

## Overview
Our client, Methanex, often rely on manual safety incident review, which slows down learning and makes it harder to detect risk patterns early. For Challenge #2, our team built a two-layer safety intelligence solution:

1. **Manager Handbook / Safety Assistant App**  
   A Streamlit-based app that lets managers describe an incident scenario and instantly retrieve:
   - similar historical cases
   - likely risk patterns
   - scenario classification
   - recommended follow-up actions from past cases

2. **Executive Safety Dashboard**  
   A Looker dashboard that gives leadership a real-time view of:
   - incident volume over time
   - risk-level trends
   - high-risk hotspots by setting
   - top action types
   - geographic distribution of incidents

Our goal was to move the safety workflow from a **reactive, case-by-case process** toward a more **proactive, scalable decision-support system**.

---

## Business Problem
Our exploratory analysis showed several important issues in the incident-management process:

- **High Risk remains the dominant category** as case volumes rise over time
- **High and Medium risk cases receive nearly the same short-term response**, suggesting urgency is not well differentiated
- **Non-minor cases are not getting meaningfully deeper follow-up**
- **Near misses are relatively rare**, limiting early learning opportunities
- The current workflow is highly manual and slow, with investigation and reporting taking weeks

These findings suggested a need for both:
- faster case-level decision support for managers, and
- better portfolio-level visibility for leadership.

---

## Solution
We designed a two-part solution:

### 1) Safety Assistant App
The app helps front-line managers move from incident description to guidance in seconds.

**Key features**
- free-text incident input
- similar case retrieval
- scenario / cluster routing
- suggested actions from comparable historical cases
- risk-level pattern summary
- optional filters such as risk level, setting, location, etc.

### 2) Executive Safety Dashboard
The dashboard helps leadership monitor systemic risk through:
- KPI summary cards
- incident trend tracking
- risk split over time
- hotspot analysis by operating setting
- top action type distribution
- country-level volume map

---

## Data pipeline
The original dataset consisted of a **500+ page PDF document of historical safety incidents and near-miss reports**. Each case contained semi-structured narrative sections such as:

- What happened
- What could have happened
- Root causes
- Causal factors
- What went well
- Lessons learned
- Corrective actions

To make the data usable for analysis and modeling, we built a preprocessing pipeline that:

1. **Parsed the raw PDF document** and extracted incident records
2. **Converted narrative sections into structured fields**
3. **Normalized action records and ownership information**
4. **Cleaned and standardized text across cases**
5. **Constructed a unified text feature (`text_for_embedding`)** combining key narrative sections

This transformation enabled downstream **EDA, clustering, semantic similarity retrieval, and action recommendation models**.

Final dataset:

- **196 safety cases**
- **1,603 corrective actions**
- Multiple structured attributes including risk level, setting, location, severity, and action ownership.

EDA and preprocessing scripts are included in this repository.

---

## Methodology

### Text processing
We cleaned and combined incident text fields, then used:
- **CountVectorizer / TF-IDF** for text exploration
- **Word2Vec** for semantic similarity
- **KMeans clustering** to group cases into common safety scenarios

### Scenario discovery
We selected **5 clusters** and mapped them into interpretable safety themes:

- Information Privacy & Confidential Exposure Risk
- AI & Automation Control Reliability Risk
- Isolation & Permit Compliance Risk
- Stored Energy & Pressure Release Hazard
- Access Control & Privilege Misuse Risk

### Retrieval & recommendation
Given a new incident description, the app:
1. converts the input into a document vector
2. assigns it to the nearest scenario cluster
3. retrieves the most similar historical cases
4. recommends actions from neighboring cases
5. summarizes action mix, timing, control type, and likely ownership patterns

### App stack
- Python
- Streamlit
- Pandas / NumPy
- Scikit-learn
- Gensim (Word2Vec)
- Vertex AI / Gemini embedding
- Looker Studio

---

## Key Insights
Some of the main findings from the dashboard and analysis include:

- High-risk cases dominate the safety record
- Industrial Operations and Utilities & Infrastructure are major hotspots
- Audit / verification actions are the most common action type
- Near misses remain underrepresented despite being valuable early warning signals
- Current follow-up patterns suggest limited differentiation by severity

---

## Team

This project was completed as part of the **Google Cloud Hackathon – Methanex Challenge** by Team 8 – *Safety in Your Area* including Thao Do, Jasmine Fu, Liz Ji, Jessica Shi. Special thanks to my teammates for their collaboration on data exploration, modeling, dashboard development, and solution design.
