# PubMed Lung Cancer Abstracts & Keywords Dataset

## Overview
This repository contains a large-scale, curated dataset of lung cancer-related abstracts extracted from PubMed, paired with their corresponding keywords. It is specifically designed to train and evaluate Natural Language Processing (NLP) models for multi-label text classification within the biomedical and oncological domains.

## Methodology & Data Collection
We used **Entrez Direct** (a tool that provides command-line access to the Entrez suite of interconnected databases, including PubMed) to query the database. The search was specifically designed to retrieve publications with titles and/or abstracts containing terms highly indicative of lung cancer. 

The queried terms included:
* "lung cancer"
* "lung neoplasms"
* "NSCLC" (non-small cell lung cancer)
* "SCLC" (small-cell lung cancer)

This targeted search yielded a massive corpus of approximately **300,000 abstracts**, providing a robust foundation for fine-tuning transformer-based architectures on complex multi-label classification tasks.

## Dataset Details
* **Source:** PubMed
* **Domain:** Oncology (Lung Cancer)
* **Task:** Multi-label Text Classification
* **Size:** ~300,000 abstracts and corresponding keyword sets
* **Language:** English

## Dataset Structure
The dataset is provided in an CSV file containing two primary columns: the abstract text and its corresponding multi-label keywords.

**Example Row:**
* **`abstract`**: *"Evaluation and modification of tumor cell isolation techniques from malignant effusions for rapid drug sensitivity testing. Non-small cell lung cancer treatment decisions rely on several diagnostic steps..."*
* **`keywords`**: `['cd45', 'drug sensitivity testing', 'epcam', 'lung cancer', 'pleural effusion', 'tumor cell isolation']`

* *Note: The `keywords` column is stored as a string representation of a Python list.*

## How to Use
You can easily load and preprocess this dataset using Python and `pandas`. Since the keywords are stored as stringified lists, you should use `ast.literal_eval` to convert them back into native Python lists for model training.

```python
import pandas as pd
import ast

# Load the dataset
df = pd.read_csv("pubmed_lung_cancer_abstracts_and_keywords.csv")

# Convert the string representation of lists back into actual Python lists
df['keywords'] = df['keywords'].apply(ast.literal_eval)

# Display the first row and verify the type
print(df.iloc[0]['abstract'])
print(df.iloc[0]['keywords'])
print(type(df.iloc[0]['keywords'])) # Output: <class 'list'>
```

## Citation

If you find this dataset useful for your research, please cite the associated Master's thesis:

@mastersthesis{dorotea2026incorporating,
  author  = "Alexandre Mestre dos Santos Aleixo Dorotea",
  title   = "Incorporating medical free text into data-driven support for lung cancer multidisciplinary team meetings",
  school  = "NOVA School of Science and Technology",
  year    = "2026",
  address = "Caparica, Portugal",
  note    = "Adviser: Filipa Valdeira, Co-adviser: Prof. Cláudia Soares"
}


