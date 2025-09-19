# 📘 Clinical Notes De-Identification & Entity Extraction App

## 1. Project Overview
This project builds an end-to-end pipeline for **de-identifying sensitive information (PHI/PII) in clinical notes** and extracting medically relevant entities.  
The system is wrapped into a **Streamlit web app** that allows users to:
- Upload clinical notes
- View masked version instantly
- Download structured outputs

---

## 2. Motivation
- Protecting patient privacy under **HIPAA** and Indian health regulations  
- Unstructured clinical notes contain sensitive identifiers (names, addresses, phone numbers, IDs)  
- Research & analytics require medical info (diseases, symptoms, medications) but without PHI  
- Demonstrates how **NLP + regex + rule-based masking** can solve this problem

---

## 3. Methodology

**Step 1 – Input Handling**  
- Users upload `.txt` clinical notes  
- App reads raw text  

**Step 2 – De-Identification Pipeline** (`deid_pipeline_fixed.py`)  
- **Regex masking**: Dates, phone numbers, emails, patient IDs, addresses & Indian cities  
- **spaCy NER masking**:
  - PERSON → `[NAME]`
  - ORG → `[ORG]` (hospital/clinic/insurance)
  - GPE/LOC/FAC → `[ADDRESS]`
  - DATE → `[DATE]`
- **Whitelist protection**: prevents masking common medical terms (e.g., fever, cough, diabetes)  

**Step 3 – Entity Extraction** (`entity_extract_pipeline.py`)  
- Extract entities relevant to clinical text: DISEASE, SYMPTOM, MEDICATION, LAB_TEST, PROCEDURE  
- Outputs structured table:

**Step 4 – Streamlit App** (`Clinical_text_mask_entity_app.py`)  
- Upload `.txt` clinical notes  
- Toggle between original and masked view  
- Highlight entities with color codes  
- Download options: masked text (`.txt`) & extracted entities (`.csv`)  
- Metrics: count of entities by type, bar chart of entity frequencies  

---

## 4. Key Features
- Privacy-preserving: masks sensitive PHI/PII  
- Preserves medical context: retains diseases, symptoms, drugs  
- Interactive UI: easy toggling & highlighting  
- Downloadable outputs for downstream ML pipelines  
- Extensible: whitelist & regex patterns can be expanded  

---

## 5. Challenges Faced
1. Over-masking (e.g., “fever” masked as `[ADDRESS]`) ✅ solved with medical-term whitelist  
2. Regex false positives ✅ balanced strictness vs flexibility  
3. NER inconsistencies ✅ added custom dictionary rules  
4. Entity overlap (e.g., “CT scan” classified as procedure & lab test) ✅ kept both categories  

---

## 6. Applications
- Hospitals/Clinics: safe sharing of de-identified patient notes  
- Medical Research: NLP studies without violating privacy  
- Healthcare Startups: build structured data lakes  
- AI Models: safely feed masked notes into clinical NLP models  

---

## 7. Future Prospects
- Integrate transformer-based de-identification models (BioBERT, ClinicalBERT)  
- Use **FHIR standard** for structured outputs  
- Build API version (FastAPI + Docker) for enterprise use  
- Multi-language support (Indian regional languages)  
- Evaluation metrics: Precision/Recall against gold annotations  
- Synthetic PHI generation for robustness testing  

---

## 8. Tech Stack
- **Python** (Regex, spaCy, Pandas)  
- **Streamlit** (Web app)  
- **Jupyter Notebook** (Prototyping)  
- **GitHub & LinkedIn** (Deployment & showcase)  

**IMAGES & SCREENSHOTS**
<img width="1810" height="643" alt="6" src="https://github.com/user-attachments/assets/bff3ba7f-0238-4499-847c-37af46822384" />
<img width="1806" height="534" alt="5" src="https://github.com/user-attachments/assets/a57f7206-5692-4697-a284-08d0f2fda8dc" />
<img width="1905" height="515" alt="4" src="https://github.com/user-attachments/assets/53fbdd93-5b03-456d-9c13-e5e24a94fd29" />
<img width="823" height="439" alt="3" src="https://github.com/user-attachments/assets/007c6871-ff15-4b23-bffc-536d263d764f" />
<img width="1833" height="756" alt="2" src="https://github.com/user-attachments/assets/76782397-7870-48ec-81ce-ab057fb51376" />
<img width="1843" height="786" alt="1" src="https://github.com/user-attachments/assets/415222dc-c308-40fd-94fe-24c339801e22" />




