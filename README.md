# Report Generation with Large Vision models.

This script runs zero-shot, one-shot, and few-shot experiments on large vision models. 

Note: The script utilizes multi-GPU parallelism. Running on thor or another GPU enabled computer is advised. 

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
#### Install rthml and rthclient
- Change directory to highest level of rthml and run the following commands. 

```bash
pip install -e rthclient \
pip install -e rthml
```

#### Install Ollama
```bash
curl -fsDh https://ollama.ai/install.sh | sh
```

#### Pull models via Ollama
```bash
ollama pull llava:7b \
ollama pull llama3.2-vision:latest
```

### Step 3: Save collection images locally
Locate `images.py` and provide:
- `collection`: The name of the collection you'd like to save images from.
- `directory`: Name of the directory to save images to.
- `num_cases`: Number of cases to save images from.

Important: ensure the image directory is saved in the same directory as the `generation.py` script.

#### Usage:
``` bash 
python3 images.py --collection ""Collection Name"" --directory ""Directory Name"" --num_cases ""Number of Cases""
```  

#### Example to save images from 10 studies:
``` bash 
python3 images.py --collection GradientHealth/LumbarSpineDegenerative --directory LumbarSpineImages --num_cases 10 
```

### Step 4: Run Model Evaluation Program
Locate `generation.py` and provide:
- `collection`: The name of the collection to run the experiment on. Be sure to use the same as `images.py`
- `num_exp`: Number of experiments to run.
- `model`: Use 'llava' to use the Llava 7b mode or 'llama' to use the Llama 3.2 vision model.
- `exp`: Use 'zero' for Zero-shot, 'one' for One-shot, and 'few' for Few-shot.
- `image_dir`: Directory path containing saved images from `images.py`

#### Usage:
``` bash 
python3 generation.py --collection ""Collection Name"" --num_exp ""Number of experiments"" --model ""Model Name"" --exp ""Shot type"" --image_dir ""Path to images""
```

#### Examples:
#### Run experiments for Llava 7b:
``` bash 
python3 generation.py --collection GradientHealth/LumbarSpineDegenerative --num_exp 5 --model llava --exp zero --image_dir LumbarSpineImages/ 
python3 generation.py --collection GradientHealth/LumbarSpineDegenerative --num_exp 5 --model llava --exp one --image_dir LumbarSpineImages/ 
python3 generation.py --collection GradientHealth/LumbarSpineDegenerative --num_exp 5 --model llava --exp few --image_dir LumbarSpineImages/ 
```

#### Run experiments for Llama3.2-vision:
``` bash 
python3 generation.py --collection GradientHealth/LumbarSpineDegenerative --num_exp 5 --model llava --exp zero --image_dir LumbarSpineImages/ 
python3 generation.py --collection GradientHealth/LumbarSpineDegenerative --num_exp 5 --model llava --exp one --image_dir LumbarSpineImages/ 
python3 generation.py --collection GradientHealth/LumbarSpineDegenerative --num_exp 5 --model llava --exp few --image_dir LumbarSpineImages/ 
```
Note: The Llama 3.2 model is heavier and might be slower for inference.
You may try to view running models, and stop via the following commands:
```bash
ollama ps
ollama stop `model-name`
```

Upon running, you will have created the following CSV files for each experiment's results:
- `zero_llava.csv`
- `one_llava.csv`
- `few_llava.csv`
- `zero_llama.csv`
- `one_llama.csv`
- `few_llama.csv`

### Results Analysis:
- The Llava 7b model demonstates strong zero-shot and few-shot accuracies but struggles for one-shot, 
  possibly due to prompt overfitting.
- The Llama3.2-vision model tends to hallucinate more in all the experiments. 
