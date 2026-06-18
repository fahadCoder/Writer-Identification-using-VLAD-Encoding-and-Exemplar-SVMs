# Historical Writer Identification using VLAD and Exemplar SVM

This project implements a classical computer vision pipeline for **historical writer identification** using the **ICDAR2017 Historical Writer Identification dataset**.

The goal is to identify documents written by the same writer by converting local document-image descriptors into global image representations and evaluating them using retrieval-based metrics.

## Overview

The project uses a **Bag of Visual Words / VLAD-based pipeline**. Local descriptors from document images are assigned to visual words, aggregated into global VLAD descriptors, normalized, and compared using cosine distance.

To improve the discriminative power of the descriptors, the project also implements **Exemplar SVMs**, where each test image is treated as a positive example and the training images are used as negative examples.

## Main Features

- Codebook generation using **MiniBatch K-Means**
- VLAD encoding from local image descriptors
- Nearest-cluster assignment using OpenCV BFMatcher
- Power normalization and L2 normalization
- Pairwise cosine-distance computation
- Retrieval evaluation using **Top-1 accuracy** and **mean Average Precision (mAP)**
- Exemplar SVM-based descriptor refinement
- Optional SIFT descriptor extraction
- Optional Hellinger normalization for SIFT descriptors
- Optional Generalized Max Pooling using Ridge Regression
- Optional multi-VLAD with PCA whitening

## Project Pipeline

```text
Local Descriptors
        |
        v
Random Descriptor Sampling
        |
        v
MiniBatch K-Means Codebook
        |
        v
VLAD Encoding
        |
        v
Power + L2 Normalization
        |
        v
Cosine Distance Retrieval
        |
        v
Top-1 Accuracy + mAP Evaluation
        |
        v
Exemplar SVM Refinement
        |
        v
Final Retrieval Evaluation
```

## Dataset

This project is based on the **ICDAR2017 Historical Writer Identification dataset**.

The dataset contains historical document images with writer labels. In this implementation, pre-computed local descriptors are used from `.pkl.gz` files for both the training and test sets.

Expected dataset structure:

```text
icdar17_local_features/
├── train/
├── test/
├── icdar17_labels_train.txt
└── icdar17_labels_test.txt
```

By default, the script expects the dataset at:

```text
/proj/ciptmp/sivichri/icdar17_local_features
```

The paths can be changed using command-line arguments.

## Technologies Used

- Python
- NumPy
- OpenCV
- scikit-learn
- tqdm
- gzip
- pickle

## Installation

Install the required Python packages:

```bash
pip install numpy scikit-learn opencv-python tqdm
```

For SIFT-based feature extraction, your OpenCV installation must support:

```python
cv2.SIFT_create()
```

## How to Run

Run the basic VLAD and Exemplar SVM pipeline:

```bash
python Solution.py
```

Run with power normalization:

```bash
python Solution.py --powernorm
```

Run with Generalized Max Pooling:

```bash
python Solution.py --gmp --gamma 1
```

Run with multi-VLAD and PCA whitening:

```bash
python Solution.py --multivlad --powernorm --n_codebooks 5 --n_clusters 100 --pca_dim 1000
```

Recompute saved codebooks and encodings:

```bash
python Solution.py --overwrite
```

Use custom dataset paths:

```bash
python Solution.py \
  --in_train /path/to/train \
  --in_test /path/to/test \
  --labels_train /path/to/icdar17_labels_train.txt \
  --labels_test /path/to/icdar17_labels_test.txt
```

## Command-Line Arguments

| Argument | Description |
|---|---|
| `--powernorm` | Applies signed square-root power normalization |
| `--gmp` | Uses Generalized Max Pooling instead of standard VLAD sum pooling |
| `--gamma` | Regularization parameter for Ridge Regression in GMP |
| `--C` | Regularization parameter for Exemplar SVM |
| `--multivlad` | Uses multiple codebooks and concatenates VLAD descriptors |
| `--n_codebooks` | Number of codebooks for multi-VLAD |
| `--n_clusters` | Number of K-Means clusters per codebook |
| `--pca_dim` | Output dimensionality after PCA whitening |
| `--overwrite` | Recomputes saved codebooks and encodings |

## Evaluation

The system evaluates writer-identification performance using:

- **Top-1 Accuracy**: checks whether the nearest retrieved document has the same writer label.
- **Mean Average Precision (mAP)**: measures the ranking quality of retrieved documents for each query.

Example output:

```text
Top-1 accuracy: X.XX - mAP: X.XX
```

## Results

| Method | Top-1 Accuracy | mAP |
|---|---:|---:|
| VLAD | TODO |
| VLAD + Power Normalization | TODO |
| VLAD + Exemplar SVM | TODO |
| VLAD + GMP | TODO |
| Multi-VLAD + PCA Whitening | TODO |
| Multi-VLAD + PCA Whitening + Exemplar SVM | TODO |

> Replace the `TODO` values with the actual results printed after running the experiments.

## What I Learned

Through this project, I learned how traditional computer vision techniques can be used for document image retrieval and writer identification.

Key learning outcomes:

- How local descriptors are converted into global image representations
- How visual vocabularies are created using K-Means clustering
- How VLAD aggregates residuals to represent an image
- Why power normalization and L2 normalization improve retrieval performance
- How cosine distance is used for image similarity search
- How mAP is used to evaluate retrieval systems
- How Exemplar SVMs can produce more discriminative descriptors
- How PCA whitening and multi-codebook VLAD can improve feature representation

## Project Structure

```text
.
├── Solution.py
├── README.md
└── results/
    └── optional_result_logs.txt
```

## Future Improvements

- Add automatic result logging
- Save all experiment outputs in a structured results file
- Add visual examples of retrieved writer matches
- Compare VLAD-based features with deep learning embeddings
- Optimize the Exemplar SVM stage for faster execution

## Author

**Your Name**

Computer Vision Project  
Historical Writer Identification using VLAD Encoding and Exemplar SVMs
