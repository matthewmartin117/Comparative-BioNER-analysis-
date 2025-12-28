# Biomedical Named Entity Recognition (BioNER): From CNNs to Transformers

## A Comparative Analysis on the BC5CDR Corpus

**Author:** Matthew Martin

**Course:** CSPB 3832

**Date:** 12/8/2025

## Project Overview

This project addresses the challenge of automated information extraction from the exponentially growing body of biomedical literature. Specifically, it implements and evaluates three distinct generations of Neural Network architectures for Named Entity Recognition (NER) to identify Chemical and Disease entities.

Using the BC5CDR (BioCreative V Chemical Disease Relation) dataset, this project investigates a key research question: *How much do modern Transformer architectures improve upon traditional CNN and RNN baselines in handling complex, multi-word biomedical nomenclature?*

[Watch the Video Presentation](https://youtu.be/A2W1aQ6QJzw)

[View the Code on Google Colab](https://colab.research.google.com/drive/1KV-5erbzHA-rYcfj_vBajgtHXDcokvKE?usp=sharing)

[Read the Complete Study] ()

## Key Findings

* **Transformers and Context:** The fine-tuned BioBERT model achieved the highest entity-level performance, specifically outperforming baselines on multi-word chemical names (e.g., "calcium channel blocker").
* **The "I-Tag" Gap:** While baselines like scispaCY had high precision for simple entities, their recall for the middle of complex names (`I-CHEMICAL`) was only 0.68. BioBERT improved this to 0.76, demonstrating the value of the self-attention mechanism for long-range dependencies.
* **Trade-offs:** scispaCY remains the superior choice for speed (inference is orders of magnitude faster), while BioBERT is the choice for maximum accuracy.

## Methodology & Architectures

I implemented three distinct models to represent the evolution of NLP:

| Architecture | Model Implementation | Characteristics | Pros/Cons |
| :--- | :--- | :--- | :--- |
| **CNN** (Convolutional Neural Network) | **scispaCY** (`en_ner_bc5cdr_md`) | Window-based feature extraction. Pre-trained on biomedical text. | Fast, Easy to Deploy; Fixed context window limits complex entity recognition. |
| **RNN** (Recurrent Neural Network) | **BiLSTM-CRF** (Custom PyTorch) | Sequential processing with bidirectional context and Character-level embeddings. | Handles sequential dependencies better than CNN; Slow training, difficult to optimize from scratch. |
| **Transformer** | **BioBERT** (`biobert-base-cased-v1.2`) | Multi-head Self-Attention mechanism. Fine-tuned on the task. | State-of-the-art accuracy, captures long-range context; Computationally expensive, requires GPU. |

## Repository Structure

* `/content/`: Directory for dataset files (BioCreative V format).
    * `bc5cdr_train.json`
    * `bc5cdr_valid.json`
    * `bc5cdr_test.json`
* **Visualizations**:
    * `comparison_table.png`: Side-by-side performance metrics of all three models.
    * `i_chemical_vs_i_disease.png`: Critical analysis chart showing the "I-Tag" performance gap.
    * `scispacy_table.png`, `bilstm_table.png`, `biobert_table.png`: Individual classification reports.

## How to Run the Code

1.  **Environment Setup**: This project is designed to run in Google Colab (GPU recommended for BioBERT training).
2.  **Download Data**: Ensure the JSON dataset files are uploaded to the `/content/` directory.
3.  **Install Dependencies**: Run the setup cells to install the required libraries.

### Dependencies
```bash
# General & Data Processing
!pip install pandas numpy matplotlib seaborn scikit-learn

# Model 1: scispaCY
!pip install scispacy spacy
!pip install https://s3-us-west-2.amazonaws.com/ai2-s2-scispacy/releases/v0.5.4/en_ner_bc5cdr_md-0.5.4.tar.gz

# Model 2: BiLSTM-CRF (PyTorch)
!pip install torch pytorch-crf seqeval

# Model 3: BioBERT (Hugging Face)
!pip install transformers datasets evaluate
```

Execution Order:
1. **Step 1:** Run the scispaCY section to establish a baseline.
2. **Step 2:** Run the BiLSTM-CRF section. Note that training from scratch may take 10-20 minutes.
3. **Step 3:** Run the BioBERT section. *Note: Ensure you are using a GPU runtime.* This section includes custom data collators and label alignment logic for sub-word tokenization.
4. **Step 4:** Run the Analysis cells to generate the comparison charts.

Future Work
* **Model Distillation:** Implement DistilBioBERT to reduce model size by 40% and increase inference speed, making the transformer approach viable for real-time applications.
* **Data Augmentation:** Address class imbalance (rare chemical names) by using synonym replacement or back-translation to generate more training examples.
* **Cross-Domain Generalization:** Test the models on the NCBI Disease Corpus to evaluate how well the BioBERT model generalizes to purely disease-focused texts.

References
* **BC5CDR Corpus:** Li et al., 2016
* **BioBERT:** Lee et al., 2020
* **scispaCY:** Neumann et al., 2019
* **BiLSTM-CRF:** Lample et al., 2016
