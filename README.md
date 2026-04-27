# PDAC Prediction CLI

A lightweight command-line tool to predict whether a sample is **PDAC (Pancreatic Ductal Adenocarcinoma)** or **non-PDAC** using gene expression (TPM) values.

The model uses a pretrained CatBoost classifier based on the expression of **5 genes**.

---

## 🧬 Model Overview

The prediction is based on the following gene set (fixed order):

- ENSG00000171345  
- ENSG00000163347  
- ENSG00000168685  
- ENSG00000151655  
- ENSG00000152601  

⚠️ These genes **must be present** in the input TPM file.

---

## 📂 Input Format

- Tabular TPM matrix  
- **Rows** → Genes (Ensembl IDs)  
- **Columns** → Samples (patients)  

### Example

| Gene ID          | Sample1 | Sample2 |
|------------------|--------|--------|
| ENSG00000171345 | 5.2    | 3.1    |
| ENSG00000163347 | 2.8    | 4.5    |
| ...              | ...    | ...    |

---

## ⚙️ Requirements

- Python ≥ 3.7  
- pandas  
- joblib  
- catboost  

Install dependencies:

```bash
pip install pandas joblib catboost
```


## 📦 File Structure

Ensure the following files are in the same directory:

.
├── predict_pdac.py  
├── scalar.joblib  
└── catboost.joblib  

---

## 🚀 Usage

Basic (TSV input):

```bash
./predict_pdac.py -i input.tsv
```

CSV input:

```bash
./predict_pdac.py -i input.csv --sep ","
```

Custom output:

```bash
./predict_pdac.py -i input.tsv -o results.csv
```
---

## 🧪 Output

The output is a CSV file containing:

- `Sample` → Sample ID  
- `Prediction` → PDAC / non-PDAC  
- `PDAC_Probability` → Probability score (if available)  

### Example

| Sample   | Prediction | PDAC_Probability |
|----------|-----------|------------------|
| Sample1  | PDAC      | 0.87             |
| Sample2  | non-PDAC  | 0.12             |

---

## 🔍 Pipeline Steps

1. Read TPM matrix  
2. Validate presence of required genes  
3. Subset genes in **exact training order**  
4. Transpose matrix (samples × genes)  
5. Scale using `scalar.joblib`  
6. Predict using `catboost.joblib`  

---

## ⚠️ Important Notes

- **Gene IDs must match exactly** (Ensembl format required)  
- **Gene order is critical** and enforced internally  
- Missing genes will result in immediate failure  
- Ensure consistency with training preprocessing (e.g., no log-transform mismatch)  
- Model and scaler must be compatible with the runtime environment  

---

## ❗ Error Handling

The tool will exit with an error if:

- Required genes are missing  
- Input format is invalid  
- Model or scaler files are not found  
- Scaling or prediction fails  

---

## 🧠 Intended Use

This tool is designed for:

- Research applications  
- Bulk transcriptomic screening  
- Integration into bioinformatics pipelines (e.g., Nextflow)  

Not intended for direct clinical decision-making without validation.

---

## 📌 License

Add your preferred license here.

---

## 👤 Author

Add your name and contact information here.
