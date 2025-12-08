# README

  

This project implements and compares three different Named Entity Recognition (NER) models for the BC5CDR dataset: scispaCy's `en_ner_bc5cdr_md`, a custom BiLSTM-CRF model, and a fine-tuned BioBERT model.

## Presentation and Overview
[Video Overview](https://youtu.be/A2W1aQ6QJzw)

  

## How to Run the Code

  

1. **Clone the Repository (if applicable)**: If this notebook is part of a larger repository, ensure you have cloned it to your environment.

2. **Download Data**: Ensure the dataset files (`bc5cdr_train.json`, `bc5cdr_valid.json`, `bc5cdr_test.json`) are placed in the `/content/` directory (or adjust the `pd.read_json` paths accordingly).

3. **Execute Cells Sequentially**: Run each code cell in the notebook from top to bottom.

* **ScispaCy Model**: The `scispacy` model is loaded and evaluated first.

* **BiLSTM-CRF Model**: The BiLSTM-CRF model is defined, trained, and evaluated next.

* **BioBERT Model**: The BioBERT model is prepared, fine-tuned, and evaluated.

* **Results Analysis**: The final cells generate comparison tables and plots.

  

## Dependencies and Setup Steps

  

Before running the notebook, ensure you have the necessary libraries installed. These are typically installed automatically by running the `!pip install` cells at the beginning of each relevant section.

  

### General Dependencies

```bash

!pip install scispacy

!pip install spacy

!pip install https://s3-us-west-2.amazonaws.com/ai2-s2-scispacy/releases/v0.5.4/en_ner_bc5cdr_md-0.5.4.tar.gz

```

  

### BiLSTM-CRF Specific Dependencies

```bash

!pip install pytorch-crf

!pip install seqeval

```

  

### BioBERT Specific Dependencies

```bash

!pip install transformers

!pip install datasets

!pip install evaluate

```

  

## Brief Description of Files and Folders

  

* **`/content/`**: This directory is expected to contain the dataset JSON files:

* `bc5cdr_train.json`: Training data for the NER task.

* `bc5cdr_valid.json`: Validation data for the NER task.

* `bc5cdr_test.json`: Test data for the NER task.

* **`scispacy_table.png`**: An image file containing the classification report for the scispaCy model.

* **`bilstm_table.png`**: An image file containing the classification report for the BiLSTM-CRF model.

* **`biobert_table.png`**: An image file containing the classification report for the BioBERT model.

* **`comparison_table.png`**: An image file containing a comparative classification report across all three models, highlighting the best scores.

* **`i_chemical_vs_i_disease.png`**: An image file visualizing the F1 scores for 'I-CHEMICAL' and 'I-DISEASE' entities across the models.
