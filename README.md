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
## Screenshots

### Step 1 – Upload File
<img width="1843" height="786" alt="1" src="https://github.com/user-attachments/assets/33af38db-6df8-4b1b-801f-9218dfce9de0" />


### Step 2 – Masking Applied
<img width="1833" height="756" alt="2" src="https://github.com/user-attachments/assets/67f5ffbd-e6fe-4d4b-bc76-fa18e84b079a" />


### Step 3 – Entity Extraction
<img width="823" height="439" alt="3" src="https://github.com/user-attachments/assets/f8921968-dae6-468f-bc7a-711ab8368133" />


### Step 4 – Results Table
<img width="1905" height="515" alt="4" src="https://github.com/user-attachments/assets/6d266a9a-fa12-4791-825c-d9e5dd2c5837" />


### Step 5 – Bar Chart & Download Options
<img width="1810" height="643" alt="6" src="https://github.com/user-attachments/assets/769e36c9-108e-4e5d-8dd1-04f0084051e6" />











