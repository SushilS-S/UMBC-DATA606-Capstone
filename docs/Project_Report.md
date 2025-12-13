# Medical Report Summarizer  
## DATA 606 – Capstone Project Report

**Student Name:** Sushil Souresh Koumar  
**Program:** MPS in Data Science, University of Maryland, Baltimore County  
**Instructor:** Dr. Chaojie (Jay) Wang  
**GitHub Repository:** 

## 1. Introduction

Medical reports, like discharge summaries and radiology notes, continue to be addressed first and foremost to the physicians. The patients and non-medical users easily find these documents challenging to comprehend due to their length, technicality, and the extensive use of medical jargon.

The project’s aim is to create and apply a **Medical Report Summarizer** that will, without losing the essential medical information, produce brief summaries from complex reports. This project is the application of contemporary NLP techniques to a healthcare issue that is tangible and pressing.

## 2. Problem Statement

The increasing usage of electronic health records has made medical documents available to patients. On the downside, these reports are still very difficult to comprehend mainly because of their complexity and heavy use of technical terms.

The main problem tackled in this project is:

-> The issue of how to create a summary of long and complicated medical reports that is not only accurate and concise but also easy to comprehend has been raised?

## 3. Project Objectives

The project aims primarily to:
- perform preprocessing and structure on the actual medical text data
- develop a basic medical text summarization system
- measure the quality of the produced summaries by applying the usual NLP metrics
- show the results of summarization via an easy-to-use interface

## 4. Dataset Description

### 4.1 Primary Dataset

**MIMIC-IV / MIMIC-III (Referenced)**  
The MIMIC dataset is one of the biggest collections of unidentifiable electronic health records that incorporates discharge summaries, radiology reports, and clinical notes from ICU patients.

PhysioNet's data use agreement allows access to the dataset under strict conditions associated with privacy and licensing and its use is for citation purposes only.

Dataset Link:  
https://physionet.org/content/mimiciv/2.2/

### 4.2 Supplementary Dataset

**OpenI Radiology Dataset**  
The dataset is open to the public and radiology reports along with medical imaging data are contained in it. It is utilized for the experimentation and validation of the summarization pipeline.

Dataset Link:  
https://openi.nlm.nih.gov/
---

## 5. Methodology

### 5.1 Data Preprocessing

The preprocessing steps performed were primarily:
- Raw medical text cleaning
- Irrelevant symbols and formatting removal
- Sentence segmentation and tokenization
- Extremely short or noisy report filtering
- Model-ready inputs structuring for text

---

### 5.2 Model Architecture

A transformer-based architecture is utilized in the project for medical text summarization. These models are pretrained on large text corpora and later fine-tuned for the speaking of the medical domain.

The most important elements are:
- A tokenizer designed to deal with lengthy medical articles
- An encoder-decoder transformer configuration
- Beam search for producing summaries

---

### 5.3 Summarization Pipeline

The summarization pipeline operates as follows:
1. Medical report as input
2. Tokenization and length normalization
3. Model inference
4. Summary generation as output

This pipeline is modular, thus making it open to upgrades and replacements of the model in future.

## 6. Implementation

### 6.1 Tools and Technologies

- Python  
- PyTorch  
- Hugging Face Transformers  
- spaCy / scispaCy  
- Streamlit  
- ROUGE evaluation metrics  

---

### 6.2 System Architecture

The system is divided into four modules that have the following functionalities:
- Data loading and preprocessing
- Model inference
- Evaluation
- User interface

Such a modular design not only facilitates maintenance but also allows for easy scaling when necessary.

## 7. Evaluation

### 7.1 Quantitative Evaluation

The effectiveness of the summarization is assessed with the metrics:
- ROUGE-1
- ROUGE-2
- ROUGE-L

The mentioned measures assess the similarity among the generated summaries and the reference ones.

---

### 7.2 Qualitative Evaluation

The inspection of summaries done by humans pays attention to:
- Key medical information being preserved
- Readability and coherence
- Unnecessary details being reduced

---

## 8. Results and Observations

The summarization model has proven to be effective in truncating the length of medical reports, but it still manages to capture the essential clinical information. The generated summaries are mainly coherent, but there are still some that are using complicated medical terms.

The outcomes show that transformer models are great for handling medical text summarization, however, they need a specific area to be fine-tuned initially.

---

## 9. Challenges and Limitations

- Unavailability of large clinical datasets
- Medical documents length going beyond the model token limits
- Complex medical terminology needing specialized resources for simplifying

All these issues are a true reflection of real-world restrictions in healthcare NLP applications.

## 10. Future Work

Among the possible enhancements for the future, one can list:
- Integrating a simplification layer that is friendly for patients
- Perfection of domain-specific models like ClinicalBERT through finetuning
- Including the assessment of the system by medical professionals
- Making the system available through cloud-based platforms

---

## 11. Conclusion

The automation of medical report summarization through modern NLP techniques was made possible as shown by the project. The system, by leveraging real-life clinical data, transformer models, and a proper evaluation setup, opens up possibilities for AI solutions in healthcare.

---
