# Polarization Identification and Analysis (Multi-Task Classification)

## 1. Project Overview

This repository documents the solution for a multi-task NLP challenge focused on identifying and characterizing polarization in social media text from two distinct languages: **English** and **Swahili**.

The project is divided into three core multi-label/binary classification tasks:

| Task | Objective | Label Columns |
|:-----|:----------|:--------------|
| **Task 1** | **Polarization Identification** | Binary: Polarized (1) vs. Non-Polarized (0) |
| **Task 2** | **Category Classification** | Multi-Label: Political, Racial/Ethnic, Religious, Gender/Sexual, Other |
| **Task 3** | **Manifestation Identification** | Multi-Label: Stereotype, Vilification, Dehumanization, Extreme Language, etc. |

## 2. Key Findings from Exploratory Data Analysis (EDA)

The EDA revealed critical linguistic and structural differences essential for the modeling strategy:

| Language | Task 1 Imbalance | Task 2 Dominance | Key Linguistic Feature | Strategic Action |
|:---------|:-----------------|:-----------------|:-----------------------|:-----------------|
| **English** | High (64% Non-Polarized) | Political (66% of tags) | Polarization often uses **complex ideological/political terms**. Text length is a **useful** feature. | Use class weighting; Use `text_len` as a feature. |
| **Swahili** | Balanced (~50% Polarized) | Racial/Ethnic (68% of tags) | Polarization often uses **generic, vulgar slang** shared across all categories. Text length is **not** a useful feature. | Use class weighting for rare categories; Treat Task 2/3 as independent binary classifiers. |

## 3. Repository Structure

```
/polarization-identification-nlp
├── .gitignore
├── README.md
│
├── /data
│   └── /raw                 # Original task data (eng.csv, swa.csv for T1, T2, T3)
│
├── /notebooks
│   ├── 01_Exploration.ipynb    # Full analysis notebook (where all insights and plots were generated)
│   └── 02_Subtask_1_eng.ipynb    # english model for task 1
│   ├── 02_Subtask_1_swa.ipynb    # swahili model for task 1
│   └── 03_Subtask_2_eng.ipynb    #english model for task 2 
│   ├── 03_subtask_2_swa.ipynb    # swahili model for task 2
│   └── 04_Subtask_3_eng.ipynb    # english model for task 3
│   ├── 04_subtask_3_swa.ipynb    # swahili model for task 3
│   
│
├── /src
│   └── utils.py                 # All reusable Python functions (Plotting, Stats, Preprocessing)
│
├── /figures                     # All generated PDF plots (for report/documentation)
│
├── /models                      # Saved model weights
│
└── requirements.txt             # Project dependencies
```

## 4. Setup and Installation

### 4.1. Prerequisites

Ensure you have Python 3.8+ installed.

### 4.2. Clone the Repository
```bash
git clone https://github.com/MELAI-1/polarization-identification-nlp.git
cd polarization-identification-nlp
```

### 4.3. Install Dependencies
It is highly recommended to use a virtual environment (`venv` or `conda`).
```bash
pip install -r requirements.txt
```

### 4.4. Data Setup (Crucial)
Place the competition data files into the `/data/raw` directory following the structure:
- `/data/raw/subtask1/train/eng.csv`
- `/data/raw/subtask2/train/eng.csv`
- `/data/raw/subtask3/train/eng.csv`
- *(and the corresponding Swahili files in each subtask folder)*

## 5. Usage (Running the EDA)

To regenerate all statistics, correlation matrices, box plots, and word clouds used in the analysis:

1. Open the main analysis notebook: `notebooks/01_Exploration.ipynb`
2. Run all cells

The generated PDF files will be saved into the `/figures` directory.

## 6. Modeling

The final modeling approach uses fine-tuned **Transformer models** (e.g., multilingual BERT or language-specific models) implemented as independent binary classifiers for Tasks 2 and 3, incorporating specific class weighting based on the imbalance identified in the EDA.

---

## 🙏 Acknowledgments

I would like to extend my deepest gratitude and sincere appreciation to the following individuals for their guidance, support, and profound influence on this project:

* **Shamsuddeen Muhammad**
* **Idris Abdulmumin**

Their invaluable teaching, direction, and expertise as my **lecturers** were instrumental in shaping the methodology and ensuring the successful completion of this analysis and modeling effort.

---

## 📧 Contact

**Author:** Astride Melvin Fokam Ninyim  
**Email:** [melvin@aims.ac.za](mailto:melvin@aims.ac.za)  
**LinkedIn:** [linkedin.com/in/astridemelvinfokamninyim11](https://www.linkedin.com/in/astridemelvinfokamninyim11/)  
**Project GitHub:** [github.com/MELAI-1/polarization-identification-nlp](https://github.com/YourUsername/polarization-identification-nlp)
