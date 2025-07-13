# Compressed-Bio_ClinicalBERT

This project focuses on developing efficient transformer-based models for automated symptom extraction from clinical text using the MIMIC-III dataset. We fine-tune Bio_ClinicalBERT on structured clinical notes to identify and classify patient-reported symptoms, aiming to enhance clinical decision support. To improve computational efficiency, we apply model compression techniques including pruning, quantization, and knowledge distillation. Our pipeline preserves strong predictive performance while significantly reducing model size and inference time.
We evaluate the models using F1 score, precision, recall, and AUROC across training epochs. The results demonstrate that optimized models can reliably extract symptoms from clinical narratives, making them suitable for deployment in resource-constrained healthcare environments.


Dataset: https://www.kaggle.com/datasets/bilal1907/mimic-iii-10k

citation
Alistair EW Johnson, Tom J Pollard, Lu Shen, Li-wei H Lehman, Mengling Feng, Mohammad Ghassemi,
Benjamin Moody, Peter Szolovits, Leo Anthony Celi, and Roger G Mark. Mimic-iii, a freely accessible
critical care database. Scientific Data, 3:160035, 2016.
