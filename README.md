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
<img width="779" height="354" alt="Screenshot 2025-09-19 111921" src="https://github.com/user-attachments/assets/cdcb6cfd-de27-4394-b0cf-3a7ebf7b23d8" />
<img width="1810" height="643" alt="Screenshot 2025-09-19 110530" src="https://github.com/user-attachments/assets/3009f1e5-0064-4ddf-b326-b0dce2c041e5" />
<img width="1806" height="534" alt="Screenshot 2025-09-19 110514" src="https://github.com/user-attachments/assets/54f4950a-1c4b-459b-bf79-0b14cb8d4080" />
<img width="1905" height="515" alt="Screenshot 2025-09-19 110457" src="https://github.com/user-attachments/assets/1c2db692-da20-4e26-ab62-1517b395b800" />
<img width="823" height="439" alt="Screenshot 2025-09-19 110424" src="https://github.com/user-attachments/assets/28a53adb-5d88-4f5a-b454-114028bd633a" />
<img width="1833" height="756" alt="Screenshot 2025-09-19 110357" src="https://github.com/user-attachments/assets/5e7ee953-dd4d-4cfc-a0c8-3b220a52f13d" />
<img width="1843" height="786" alt="Screenshot 2025-09-19 110329" src="https://github.com/user-attachments/assets/aebe2a6e-928f-418b-b9ee-541554daf172" />
