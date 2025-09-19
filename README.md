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
<img width="1810" height="643" alt="6" src="https://github.com/user-attachments/assets/e4cae307-1bd9-4d50-b270-caab2f8fa805" />
<img width="1806" height="534" alt="5" src="https://github.com/user-attachments/assets/3f98c087-8e03-4eab-ab3f-ac8c1e02b1a1" />
<img width="1905" height="515" alt="4" src="https://github.com/user-attachments/assets/89034403-e1c5-4f95-9602-b2fdaf9da7be" />
<img width="823" height="439" alt="3" src="https://github.com/user-attachments/assets/d18b6dce-cfe4-45c3-92ee-c45a43484860" />
<img width="1833" height="756" alt="2" src="https://github.com/user-attachments/assets/aa88f56f-00a0-4b67-8304-bb66d6a472f0" />
<img width="1843" height="786" alt="1" src="https://github.com/user-attachments/assets/48a86c02-7b31-4600-a6f3-3d21d0dd6981" />





