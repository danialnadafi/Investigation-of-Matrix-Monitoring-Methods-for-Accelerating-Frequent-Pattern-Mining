<div align="center">

# Matrix Monitoring & Sketching for Streaming Transaction Data  
**Dimensionality Reduction • Streaming Analysis • Pattern Preservation**

**Main Notebook:** `CDM_1_Final.ipynb`  

**Dataset:** UCI Online Retail Dataset  
**Author:** Danial Nadafi  
**University:** Amirkabir University of Technology (Tehran Polytechnic)  
**Course:** Computational Data Mining  
**Instructor:** Dr. Mehdi Ghatee  

</div>

---

## Prerequisites
- **Python 3.8+**
- **pip** (Python package manager)
- **Jupyter Notebook** or **JupyterLab**

---

## Project Overview
This repository presents a complete, academic-level implementation and evaluation of **matrix monitoring and sketching techniques** for **large-scale streaming transaction data**.

The main objective is to analyze how different low-rank approximation methods behave under **incremental data arrival**, and how well they preserve:
- matrix structure  
- frequent itemsets  
- anomaly signals  

while operating under strict **time and memory constraints**.

All experiments are conducted on the **UCI Online Retail** dataset using a transaction–item matrix representation.

---

## Core Methods Implemented

The project compares three fundamentally different sketching approaches with sketch size **k = 20**:

| Method | Category | Description |
|------|----------|-------------|
| **GRP (Gaussian Random Projection)** | Randomized | Projects data using a Gaussian random matrix. Extremely fast but weak at preserving variance and structure. |
| **IPCA (Incremental PCA)** | Statistical | Incrementally updates principal components. Produces high-quality reconstructions but is computationally expensive. |
| **SpFD (Sparse Frequent Directions)** | Deterministic | Combines sparse embedding with Frequent Directions to balance accuracy and efficiency. |

Each method processes the data **incrementally**, simulating a real streaming environment.

---

## Installation & Quick Start

```bash
git clone https://github.com/your-username/matrix-monitoring-sketching.git
cd matrix-monitoring-sketching
pip install numpy pandas scipy scikit-learn matplotlib mlxtend jupyter
jupyter notebook CDM_1_Final.ipynb
```

---

## Reproducibility
The notebook is fully reproducible and can be executed **top-to-bottom** without modification.

---

## Dataset Description
- **Source:** UCI Machine Learning Repository – Online Retail  
- **Raw Transactions:** 541,909  
- **After Cleaning:** 390,892  

**Final Matrix Dimensions**
- **Rows (Invoices):** 18,404  
- **Columns (Items):** 3,658  

Transactions are sorted chronologically and split into **10 streaming batches**.

---

## Experimental Pipeline

### Phase 1 – Data Cleaning & Matrix Construction
- Remove invalid transactions (negative quantities, missing fields)
- Construct an **Invoice × Item** transaction matrix
- Convert timestamps into a chronological streaming order

### Phase 2 – Matrix Monitoring & Sketching
For each incoming batch:
- Update the sketch
- Reconstruct the approximate matrix
- Measure:
  - **Reconstruction error (Frobenius norm)**
  - **Captured variance ratio**
  - **Cumulative runtime**

### Phase 3 – Frequent Pattern Mining
- Apply **FP-Growth** on:
  - Original matrix
  - GRP sketch
  - IPCA sketch
  - SpFD sketch
- Compare number of patterns, support statistics, and runtime

### Phase 4 – Anomaly Injection & Detection
- Inject synthetic anomalous transactions into selected batches
- Monitor reconstruction error over time
- Evaluate anomaly visibility across different sketching methods

---

## Key Results & Insights

### Reconstruction Quality
- **IPCA** achieves the lowest reconstruction error  
- **SpFD** closely matches IPCA  
- **GRP** loses significant structural information  

### Runtime Performance
- **GRP:** fastest by a large margin  
- **IPCA:** slowest but most accurate  
- **SpFD:** best accuracy–efficiency tradeoff  

### Frequent Pattern Preservation

| Method | Patterns Found | Fidelity |
|------|----------------|----------|
| Original | 20 | Ground truth |
| GRP | 1 | Very poor |
| IPCA | 19 | Excellent |
| SpFD | 18 | Very strong |

### Anomaly Detection
- **GRP** produces strong anomaly signals in reconstruction error  
- **IPCA / SpFD** are more stable under injected anomalies  

---

## Visualizations Included
- Variance ratio vs time  
- Reconstruction error vs time  
- Cumulative runtime comparison  
- Frequent itemset statistics  
- Anomaly detection timelines  

---

## Why This Project Matters
This project highlights that:
- Fast sketches may fail for downstream mining  
- Accuracy alone is insufficient if runtime explodes  
- **Frequent Directions–based methods** provide an excellent compromise  
- Sketch choice directly impacts real analytical outcomes  

---

## Repository Structure
```text
.
├── CDM_1_Final.ipynb
├── data/
│   └── Online Retail.csv
└── README.md
```

---

## Notes & Limitations
- Variance ratios for **GRP** and **SpFD** are approximations and not directly comparable to PCA explained variance  
- **FP-Growth** requires binarization; thresholds affect results  
- Anomaly sensitivity depends on injected anomaly design  

---

## Citation
- **Dataset:** UCI Machine Learning Repository – Online Retail  
- **Algorithms:**
  - Gaussian Random Projection  
  - Incremental PCA  
  - Frequent Directions  

---

⭐ **If this repository helped you understand streaming sketching and data mining, consider starring it!**

Happy coding,  
**Danial Nadafi**
