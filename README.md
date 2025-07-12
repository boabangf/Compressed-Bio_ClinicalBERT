# Compressed-Bio_ClinicalBERT

This project focuses on developing efficient transformer-based models for automated disease diagnosis using clinical text data from the MIMIC-III dataset. 
We fine-tune Bio_ClinicalBERT on structured discharge summaries to classify patient diagnoses, aiming to support clinical decision-making. 
To improve computational efficiency, we apply model compression techniques including pruning, quantization, and knowledge distillation.
Our pipeline maintains strong predictive performance while significantly reducing model size and inference time. 
We evaluate the models using F1 score, precision,  recall and AUROC across training epochs. 
Results show that optimized models can reliably perform disease diagnosis from clinical notes,
making them well-suited for deployment in real-world, resource-limited healthcare settings.

Symptom Extraction Instructions (ClinicalBERT Multiclass Version)
🔧 1. Install Dependencies
Ensure you have Python ≥3.8 and install required packages:

bash
Copy
Edit
pip install transformers datasets scikit-learn pandas torch
If you're using Jupyter or Colab, run:

bash
Copy
Edit
!pip install transformers datasets scikit-learn pandas torch
📁 2. Prepare Your Dataset
You should have a file named:

NOTEEVENTS_random_chatgpt.csv (sampled subset of MIMIC-III clinical notes)

This file must contain a column:

"TEXT" — a string of clinical notes.

The code extracts a single symptom label per document by checking whether one of the following symptoms is present:

python
Copy
Edit
symptom_list = ["fever", "cough", "headache", "nausea", "vomiting"]
The model assigns a unique class (label) based on the first matching symptom found in the text.

🧹 3. Data Preprocessing and Labeling
Your script:

Converts text to lowercase

Checks for presence of symptoms

Assigns a label index (0 to 4) depending on the first matched symptom

Drops samples with no matching symptoms

No manual annotation is required!

🧠 4. Model Training
The code fine-tunes five versions of emilyalsentzer/Bio_ClinicalBERT:

Version	Description
Base	Standard Bio_ClinicalBERT
Pruned	Linear layers sparsified by 30%
Low-Rank	Linear layers decomposed with SVD (rank=8)
Quantized	Dynamically quantized model (int8 weights)
Distilled	Knowledge distillation from teacher model

Each model:

Trains for 5 epochs

Uses CrossEntropyLoss for multiclass classification

Tracks metrics per epoch: accuracy, precision, recall, F1, AUROC

Saves metrics to .csv (e.g. multiclass_base_metrics.csv)

📈 5. Evaluation
After each epoch, the model is evaluated on a held-out test set using:

Accuracy

Macro Precision, Recall, F1

AUROC (One-vs-Rest for multiclass)

Metrics are printed and also saved in CSV format for later comparison.

▶️ 6. How to Run Everything
To launch all experiments sequentially, run:

bash
Copy
Edit
python your_script.py
This calls:

python
Copy
Edit
run_all()
Which executes:

python
Copy
Edit
base_model()
pruning_model()
lowrank_model()
distillation_model()
quantization_model()
📊 7. Check Results
Each model’s evaluation results are written into a CSV file:

multiclass_base_metrics.csv

multiclass_pruning_metrics.csv

etc.

You can use pandas or Excel to analyze them, or plot trends (e.g., accuracy vs method).

🔁 Optional: Expand to More Symptoms
You can extend the list of symptoms:

python
Copy
Edit
symptom_list = ["fever", "cough", "headache", "nausea", "vomiting", "fatigue", "dizziness", "chills"]
Be sure to retrain the models after this change.
