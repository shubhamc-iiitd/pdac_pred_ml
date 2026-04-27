# PDAC Prediction Tool

This tool is a Python-based Command Line Interface (CLI) designed to predict **Pancreatic Ductal Adenocarcinoma (PDAC)** status from gene expression data. It utilizes a machine learning pipeline involving a pre-trained **CatBoost** model and a **StandardScaler** to classify samples based on a specific 5-gene signature.

## Requirements

To run this tool, you need the following Python libraries installed:
* **pandas**: For data manipulation and processing.
* **joblib**: For loading the serialized model and scaler files.
* **catboost**: Required to run the inference model.
* **scikit-learn**: Necessary for the `StandardScaler` functionality.

## Files and Directory Structure

The script identifies paths relative to its own location. Ensure the following files are in the same directory:
* `pdac_pred.py`: The execution script.
* `scaler.joblib`: The pre-trained scaling object.
* `catboost_model.joblib`: The trained CatBoost model.

## Gene Signature

The model specifically requires **TPM (Transcripts Per Million)** values for these five Ensembl Gene IDs:
1. `ENSG00000171345`
2. `ENSG00000163347`
3. `ENSG00000168685`
4. `ENSG00000151655`
5. `ENSG00000152601`

## Usage

Run the tool from the command line using the following syntax:

```bash
python pdac_pred.py -i <input_file> -o <output_file> --sep <delimiter>
```

Arguments:
-i, --input: (Required) Path to the input TPM file (format: genes x samples).

-o, --output: (Optional) Name of the output CSV file. Defaults to predictions.csv.

--sep: (Optional) The delimiter used in your input file. Defaults to \t (Tab). Use , for CSV files.
