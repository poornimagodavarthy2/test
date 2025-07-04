# NLP Pipeline to extract doctor's notes to JSON

This script generates structured JSON outputs from a specified collection and saves to a CSV.

## Setup Instructions
### Step 1: Create a virtual environment

```bash
python3 -m venv venv
source venv/bin/activate
```
### Step 2: Install dependencies
```bash
pip install -r requirements.txt
```
#### Pull model via Ollama
```bash
ollama pull llama3:8b
```
### Step 3: Run Program
To run the program, you need to provide:
- `collection_name`: The name of the collection you'd like to run the pipeline on.
- `report_title`: Report name to use for saving CSV file and generating reports.

#### Usage:
``` bash 
python3 NLP_pipeline.py --collection_name "Collection Name" --report_name "Report Name"
```

#### Example:
``` bash 
python3 NLP_pipeline.py GradientHealth/LumbarSpineDegenerative LumbarSpineDegenerative
```
