# Clinical Notes De-Identification and Entity Extraction

This project focuses on **automatically detecting and masking sensitive entities in clinical notes** (such as names, addresses, contact details, and IDs) while preserving medical information like symptoms and diagnoses.  
It also provides a **Streamlit-based web app** to test the pipeline, visualize entity counts, and download de-identified text.

---

## 🚀 Features
- Named Entity Recognition (NER) with **spaCy**
- Custom logic to avoid false positives (e.g., ensuring symptoms like "fever" are not masked)
- Masking of PHI (Protected Health Information) entities such as:
  - Names  
  - Addresses  
  - Contact info  
  - IDs  
- Entity statistics table (entity, type, count)
- Bar chart visualization of entity counts
- Downloadable de-identified text
- Interactive **Streamlit Web App**

---

## 📂 Project Structure
MedicalNER-Deidentification/
│── app/
│ ├── Clinical_text_mask_entity_app.py # Streamlit app
│ ├── deid_pipeline_fixed.py # De-identification pipeline
│ ├── entity_extract_pipeline.py # Entity extraction pipeline
│ ├── requirements.txt # Dependencies
│
│── notebooks/
│ ├── deid_clinical_notebook.ipynb # De-identification exploration
│ ├── entity_extraction_notebook.ipynb # Entity extraction exploration
│
│── data/
│ ├── Clinical_text.txt # Sample clinical note
│ 
│
│── docs/
│ ├── project_report.md # Detailed project writeup
│ ├── images/ # Screenshots
│
│── README.md # Project overview