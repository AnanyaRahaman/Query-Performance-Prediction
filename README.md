# Query Performance Prediction

This project explores whether SQL query performance can be predicted directly from query text using a Transformer-based model. It fine-tunes **BERT (`bert-base-uncased`)** to classify SQL queries into performance categories based on labeled examples. The main goal is to identify potentially expensive queries early and support database performance analysis.

The project uses SQL workloads from the **SDSS dataset** and frames runtime prediction as a **binary classification task**. Queries are labeled using the `Original` column, where `YES` and `NO` are converted into numeric labels for model training and evaluation.

## Project Objectives

- Predict SQL query performance from query text
- Fine-tune a Transformer model for SQL runtime classification
- Evaluate model behavior on both single-query and CSV-based test inputs
- Explore whether query text alone contains enough signal to estimate performance

## Dataset

This project uses SQL query data from the **SDSS workload**.

### Expected columns
The training and test CSV files should contain:

- `SQL_Statement` → the SQL query text
- `Original` → binary label (`YES` / `NO`)

In the notebook:
- `YES` is mapped to `1`
- `NO` is mapped to `0`

### Example files used
- `subset_runtime_dataset_transformer.csv` → training/evaluation dataset
- `sdss_runtime.csv` → test dataset

> If your dataset is too large, you may keep it outside the repository and add instructions for local placement.

## Approach

The notebook fine-tunes **BERT for sequence classification** using SQL query text as input. It uses the Hugging Face `transformers` and `datasets` libraries.

### Workflow
1. Load the dataset from CSV
2. Keep only `SQL_Statement` and `Original`
3. Convert labels from `YES/NO` to `1/0`
4. Split the dataset into train and test sets
5. Tokenize SQL queries using `BertTokenizer`
6. Fine-tune `BertForSequenceClassification`
7. Evaluate the model
8. Test the trained model on:
   - a single SQL query
   - a CSV file of SQL queries

## Technologies Used

- Python
- Jupyter Notebook
- Pandas
- NumPy
- Hugging Face Transformers
- Hugging Face Datasets
- PyTorch
- Accelerate
- Scikit-learn

## Model Configuration

The notebook uses the following setup:

- **Model:** `bert-base-uncased`
- **Task:** Binary classification
- **Learning rate:** `3e-5`
- **Train batch size:** `8`
- **Eval batch size:** `16`
- **Epochs:** `3`
- **Weight decay:** `0.01`
- **Max token length:** `512`


├── results/
├── README.md
└── requirements.txt
