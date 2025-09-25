# Medical Report Summarizer  
DATA 606: Capstone Project  
Faculty: Dr. Chaojie (Jay) Wang  

**Author:** Sushil Souresh Koumar

**GitHub Repository:** https://github.com/SushilS-S/UMBC-DATA606-Capstone  
**LinkedIn Profile:** https://www.linkedin.com/in/sushils-s/ 

---

## 2. Background  

Modern healthcare generates enormous amounts of unstructured text — clinical notes, radiology reports, and discharge summaries. While these records are essential for physicians, they are often filled with medical jargon that is hard for patients and families to understand. This communication gap can lead to confusion, poor treatment adherence, and lack of trust in the healthcare system.  

This project addresses the challenge by applying **large language models (LLMs)** to generate **patient-friendly summaries** of medical reports. The aim is not to alter diagnoses or prescribe treatments, but to transform complex reports into plain English, improving comprehension and supporting informed decision-making.  

### Why does it matter?  
Patients frequently leave hospitals with discharge papers they cannot interpret. Misunderstanding instructions can delay recovery, increase readmission rates, or even cause harm. On the other side, clinicians have limited time to simplify technical notes manually. An automated summarizer provides clear explanations, saves clinician effort, and builds patient trust.  

---

## Research Questions  

1. Can LLMs trained on clinical notes produce concise, accurate, and patient-friendly summaries?  

2. Which medical terms need the most frequent simplification (e.g., “myocardial infarction” → “heart attack”)?  

3. How does the readability of AI-generated summaries compare to original clinical notes?  


---

## 3. Data  

### Sources  
- **MIMIC-IV Note (v2.2)** — de-identified ICU clinical notes and discharge summaries from PhysioNet.  
- **PubMed abstracts** — scientific articles with abstracts serving as ground-truth summaries.  
- **MedlinePlus / Healthline** — plain-language medical articles for training simplification.  

### Size  
- MIMIC-IV Note: ~2 million notes (depending on filters).  
- PubMed abstracts: millions available via API.  
- MedlinePlus: thousands of patient-facing health articles.  

### Unit of Observation  
- Each row = one clinical note or report (with optional paired summary).
- 
| Column Name  | Data Type | Definition                               | 
|--------------|-----------|------------------------------------------|
| subject_id   | int       | Patient identifier (de-identified)       | 
| hadm_id      | int       | Hospital admission ID                    | 
| note_id      | int       | Unique note ID                           | 
| chartdate    | date      | Note date                                | 
| category     | string    | Note type                                | 
| description  | string    | Sub-category of note                     | 
| text         | string    | Full free-text note content              | 

---
