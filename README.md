# Clinical BERT for Report Validation

This script computes precision, recall, and F1 for model-generated clinical reports.

## Setup Instructions
### Step 1: Create a virtual environment

```bash
python3 -m venv venv --system-site-packages
source venv/bin/activate
```
### Step 2: Install dependencies
```bash
pip install -r requirements.txt
```

### Step 3: Prepare Keywords File
Create a `keywords.yaml` file with medical keywords, or use the one provided for lumbar spine.

### Step 4: Run program:
#### Option 1: Score CSV file 
Process multiple reports from a CSV file containing model outputs and ground truth.

Usage:
```bash
python3 clinical_bert.py -f --collection_name "Collection Name" --filepath "path/to/your/file.csv" --filename "results.csv"
```
Required CSV format:
- `Model Output`: Column containing generated clinical reports.
- `Ground Truth`: Column containing ground truth clinical reports. 

Example:
```bash
python3 clinical_bert.py -f --collection_name LumbarSpineVectorDB --filepath Sample_Reports.csv --filename ClinicalBertResults.csv 
```
#### Option 2: Import and use programatically
Import Clinical BERT evaluation in your own python scripts:
```python
import chromadb
from clinical bert import clinical_bert, initialize_vectorDB, query_vectorDB

# Initialize vector database
client = chromadb.PersistentClient(path="./my_collection")
initialize_vectorDB("my_collection", client)

# Evaluate reports
results = clinical_bert(model_output, ground_truth)
```

Command Line Arguments:
- `-f, --file`: Flag to enable CSV file processing.
- `collection_name`: Name for ChromaDB collection.
- `filepath`: Path to input CSV file, if used. 
- `collection_name`: Output filename for results CSV if used. 

Results:
Returns a dictionary with evaluation metrics.
```python
{
    'Precision' : 0.857,
    'Recall' : 0.750,
    'F1' : 0.800

}
```
