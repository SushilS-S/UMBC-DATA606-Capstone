# DATA 606 – Capstone Project Report
### Prepared for: UMBC Data Science Master’s Degree Capstone Instructor: Dr. Chaojie (Jay) Wang 
### Author: Sushil Souresh Koumar


## 1. Title and Author
### Project Title: Medical Report Summarizer 
**GitHub Repository:** [Repository](https://github.com/SushilS-S/UMBC-DATA606-Capstone)  
**LinkedIn:** [Sushil S](https://www.linkedin.com/in/sushils-s/)  
**PPT:** [Presentation](https://umbc-my.sharepoint.com/:p:/g/personal/sushils2_umbc_edu/IQAaMWnKuCXfR7A2EK7ZifzGAdEUk1XOtYfNyraqViamstM?e=ue7FVq)  
**YouTube Video:** [Video](https://youtu.be/uJ1DiCt-isk)


## 2. Background

Medical reports, like discharge summaries and radiology notes, continue to be addressed first and foremost to the physicians. The patients and non-medical users easily find these documents challenging to comprehend due to their length, technicality, and the extensive use of medical jargon.

The project’s aim is to create and apply a **Medical Report Summarizer** that will, without losing the essential medical information, produce brief summaries from complex reports. This project is the application of contemporary NLP techniques to a healthcare issue that is tangible and pressing.

The increasing usage of electronic health records has made medical documents available to patients. On the downside, these reports are still very difficult to comprehend mainly because of their complexity and heavy use of technical terms.

The main problem tackled in this project is:

-> The issue of how to create a summary of long and complicated medical reports that is not only accurate and concise but also easy to comprehend has been raised?

The main objectives of this project are:
- To preprocess and structure real-world medical text data
- To build a baseline medical text summarization system
- To evaluate the quality of generated summaries using standard NLP metrics
- To present the summarization results through a simple interface

## 3. Dataset Description

### 3.1 Primary Dataset

**MIMIC-IV / MIMIC-III (Referenced)**  
The MIMIC dataset is one of the biggest collections of unidentifiable electronic health records that incorporates discharge summaries, radiology reports, and clinical notes from ICU patients.

PhysioNet's data use agreement allows access to the dataset under strict conditions associated with privacy and licensing and its use is for citation purposes only.

Dataset Link:  
https://physionet.org/content/mimiciv/2.2/

### 3.2 Supplementary Dataset

**OpenI Radiology Dataset**  
The dataset is open to the public and radiology reports along with medical imaging data are contained in it. It is utilized for the experimentation and validation of the summarization pipeline.

Dataset Link:  
https://openi.nlm.nih.gov/
---

## 4. Exploratory Data Analysis (EDA)

### 4.1 Dataset Overview

The dataset used in this project consists of medical text documents containing detailed clinical information recorded by healthcare professionals. These documents include narrative descriptions of patient conditions, observations, diagnoses, and medical decisions. The text is unstructured, domain-specific, and rich in medical terminology.

Initial inspection confirmed that the dataset reflects real-world clinical documentation. The presence of long narrative reports indicates that manual summarization would be time-consuming and inconsistent, reinforcing the need for automated summarization methods.

### 4.2 Text Length Distribution

<img width="860" height="479" alt="image" src="https://github.com/user-attachments/assets/b06a640d-190c-4171-876c-f94e7e8ad956" />
<img width="860" height="479" alt="image" src="https://github.com/user-attachments/assets/b5cf85b6-8f55-4d70-8109-a66b142aa875" />

The figure compares the word count distributions of the original medical questions and their corresponding summarized versions. The original questions exhibit a wide and right-skewed distribution, with many texts extending beyond 100 words and some exceeding 200 words, highlighting the verbose and variable nature of raw medical documentation. In contrast, the summarized questions are tightly clustered within a much narrower range, primarily between 7 and 12 words, with very few summaries exceeding 20 words. This substantial reduction in length demonstrates the effectiveness of the summarization process in producing concise and consistent outputs. The clear separation between the two distributions confirms that the dataset is well-suited for training and evaluating models aimed at generating brief, focused, and patient-friendly medical summaries.


### 4.3 Compression Ratio 
<img width="720" height="427" alt="image" src="https://github.com/user-attachments/assets/133ddf7f-a875-4875-9219-a85e08afa001" />
The figure illustrates the compression ratio between the summarized text and the original medical questions, measured as the ratio of target length to source length. The distribution is tightly concentrated, with a median compression ratio of approximately 0.02–0.03, indicating that the generated summaries are roughly 30 to 50 times shorter than the original inputs. The narrow interquartile range suggests strong consistency in summary length across most samples, while a small number of higher-value outliers reflect cases where slightly longer summaries were required. Overall, this analysis confirms that the dataset supports a highly abstractive summarization task, where long and complex medical questions are consistently condensed into short, precise, and information-dense summaries.

### 4.4 Novelty and ROUGE-L Score Distributions
<img width="1784" height="584" alt="image" src="https://github.com/user-attachments/assets/a4325053-db47-43ef-8471-615f070aa52a" />
The figure presents the distribution of novelty scores and ROUGE-L F1 overlap between the source texts and their corresponding summaries. The bigram and trigram novelty distributions are concentrated at 100%, indicating that nearly all n-grams in the summaries do not appear in the original texts. This suggests that the summaries are highly abstractive and rely on new phrasing rather than copying sequences from the source documents. In contrast, the ROUGE-L F1 scores are extremely low and tightly clustered near zero, showing minimal direct overlap between the source and summary texts. Together, these results confirm that the dataset represents a strongly abstractive summarization task, where summaries are rewritten interpretations of the original medical questions rather than extractive or compressed versions of the input.

### 4.5 Section-Level Contribution of Summary Sentences
<img width="1006" height="744" alt="image" src="https://github.com/user-attachments/assets/bc947e1f-9323-4585-b7f4-0f62e2caa8ac" />
The figure shows the section-level contribution analysis, indicating which parts of the dataset most strongly align with the content of the generated summaries. The results reveal that the vast majority of summary sentences are sourced from the **target** section, which represents the ground-truth human-written summaries. This dominant contribution confirms that the summaries are aligned with the intended reference outputs rather than being influenced by auxiliary numerical features such as word count, character count, readability scores, or compression ratios. The negligible contribution from these metadata-related sections highlights a clear separation between content-bearing text and statistical features. Overall, this analysis validates that the summarization task is driven by meaningful textual information and that the model learning process focuses on semantic content rather than derived numerical attributes.

## 5. Model Training

### Models Used

This project focuses on **abstractive text summarization** and uses transformer-based sequence-to-sequence models aligned with the Recsum framework. The primary approach relies on pretrained encoder–decoder architectures available through the **Hugging Face Transformers** library. These models are suitable for summarization because they can learn to rewrite long medical texts into concise summaries rather than simply extracting sentences.

The project emphasizes the summarization pipeline and evaluation rather than extensive multi-model benchmarking.

---

### Training Approach

The model training follows a supervised learning setup, where:
- The **source medical text** (original question or report) is used as input.
- The **target text** (human-written summary) is used as the output.

Text is tokenized, padded, and truncated to meet model input constraints. Training optimizes sequence-to-sequence loss to minimize the difference between generated summaries and reference summaries. The focus is on learning concise and meaningful representations rather than maximizing lexical overlap.

---

### Train–Test Split

An **80/20 train–test split** is used:
- 80% of the data for training
- 20% of the data for evaluation

This split ensures sufficient data for learning while allowing reliable performance analysis on unseen samples.

---

### Python Packages Used

Only the libraries actively used in the project are listed below:
- **PyTorch** – model training and inference
- **Hugging Face Transformers** – pretrained summarization models and tokenizers
- **Pandas & NumPy** – data processing and analysis
- **NLTK** – text preprocessing utilities
- **ROUGE-score** – evaluation of summarization quality
- **Matplotlib & Seaborn** – exploratory data analysis and visualization

---

### Development Environment

Development and experimentation were conducted using:
- **Local machine (laptop)** for data preprocessing and EDA
- **Google Colab** for running compute-intensive training tasks
- **GitHub** for version control, documentation, and project presentation

This setup balances ease of experimentation with reproducibility.

---

### Model Evaluation

Model performance is evaluated using metrics that align with the project goals:
- **ROUGE-L F1** to measure structural similarity between source and summary
- **Compression ratio** to quantify how much the text is condensed
- **Novelty (bigram and trigram novelty)** to assess abstractiveness
- **Qualitative inspection** to ensure summaries are coherent and medically relevant

These metrics emphasize abstraction and conciseness rather than direct text overlap.

---

## 6. Application of the Trained Model

A simple **web-based application** is developed to demonstrate interaction with the trained summarization model. The application allows users to input a medical question or report and receive a generated summary.

**Streamlit** is used for the web interface due to its simplicity and tight integration with Python-based machine learning workflows. The application serves as a proof-of-concept, showing how the summarization model can be used in real-world scenarios such as patient-facing tools or clinical documentation review.

---

## 7. Conclusion

### Summary of Work

This project presents an end-to-end medical text summarization pipeline, including exploratory data analysis, model training, evaluation, and application development. The analysis shows that the dataset contains long, complex, and low-readability medical text, making it well-suited for abstractive summarization. The trained model successfully produces concise summaries that significantly reduce text length while maintaining consistency.

---

### Limitations

The project has several limitations:
- Restricted access to large-scale clinical datasets
- Input length constraints of transformer models
- Lack of expert medical validation for generated summaries
- No explicit patient-friendly simplification layer implemented

---

### Lessons Learned

Key lessons learned include:
- The importance of domain-specific data in healthcare NLP
- The trade-off between abstraction and factual overlap
- Practical challenges in handling long medical documents
- The value of combining statistical evaluation with qualitative analysis

---

### Future Research Directions

Future work can extend this project by:
- Adding medical jargon simplification for patient-friendly summaries
- Fine-tuning domain-specific models for clinical text
- Incorporating human-in-the-loop evaluation
- Deploying the application on cloud platforms

---

## 8. References

- Johnson, A. E. W., et al. *MIMIC-IV: A Freely Accessible Electronic Health Record Dataset*
- Hugging Face Transformers Documentation  
  https://huggingface.co/docs
- OpenI Radiology Dataset  
  https://openi.nlm.nih.gov/
- ROUGE: A Package for Automatic Evaluation of Summariesx
