# ReguSum: Regulatory Summarization Dataset

This repository contains the **ReguSum dataset** and scripts for preparing U.S. regulatory documents for summarization research.  
The dataset is derived from **SEC (Securities and Exchange Commission)** and **IRS (Internal Revenue Service)** regulatory filings collected from [regulations.gov](https://www.regulations.gov/) (2020–2024).  
We provide both the dataset (`regusum_dataset.json`) and utilities for preprocessing, segmentation, and dataset analysis.

---

## 📂 Repository Structure

```
├── ReguSum_Data_Preparation.ipynb   # Colab notebook (data collection, parsing, segmentation, statistics)
├── data/                            # Local working folder (CSV, HTML, JSON)
├── stats/                           # Aggregate statistics + plots
│   ├── regusum_stats.csv
│   ├── regusum_doc_length_distribution.csv
│   ├── regusum_sum_length_distribution.csv
│   ├── doc_length_hist.png
│   ├── summary_length_hist.png
│   ├── doc_length_ecdf.png
│   └── ...
└── README.md
```

---

## 🚀 Data Preparation Pipeline

1. **Download CSV metadata** from the [Bulk Data Download](https://www.regulations.gov/) section.  
   - Agencies: SEC, IRS  
   - Timeframe: 2020–01–01 to 2024–12–31  

2. **Parse and fetch HTML content**  
   - Only `.htm/.html` files are kept (skip PDFs).  
   - Saved as `<DocumentID>.htm`.

3. **Parse regulatory HTML**  
   - Extract **gold summaries** (from `SUMMARY:` blocks).  
   - Segment `SUPPLEMENTARY INFORMATION` into sections using hierarchical splitting.  
   - Discard documents with missing/empty summaries.

4. **Save dataset**  
   - Final dataset is stored in `regusum_dataset.json`.

5. **Generate statistics**  
   - Aggregate stats, word/sentence counts.  
   - Length distributions + plots.  

---

## 📊 Dataset Statistics

**Aggregate Statistics**

| Agency | #Docs | Avg Doc Words | Avg Doc Sentences | Avg Summary Words | Avg Summary Sentences | Avg Sections |
|--------|-------|----------------|-------------------|-------------------|-----------------------|--------------|
| IRS    | 205   | 26,929.4       | 826.5             | 156.8             | 6.4                   | 6.20         |
| SEC    | 140   | 67,379.7       | 1541.5            | 159.7             | 5.1                   | 8.50         |
| **Total** | **345** | **43,344.0** | **1116.6** | **158.0** | **5.9** | **7.11** |

---

**Document Length Distribution (Word Tokens)**

| Agency | 0–128 | 128–256 | 256–512 | 512–1024 | 1024–2048 | 2048–4096 | 4096–8192 | 8192+ |
|--------|-------|---------|---------|----------|-----------|-----------|-----------|-------|
| IRS    | 1     | 23      | 17      | 21       | 10        | 14        | 23        | 96    |
| SEC    | 2     | 6       | 5       | 3        | 8         | 20        | 12        | 84    |
| **Total** | **3** | **29** | **22** | **24** | **18** | **34** | **35** | **180** |

---

**Summary Length Distribution (Word Tokens)**

| Agency | 0–128 | 128–256 | 256–512 | 512–1024 | 1024–2048 | 2048–4096 | 4096–8192 | 8192+ |
|--------|-------|---------|---------|----------|-----------|-----------|-----------|-------|
| IRS    | 110   | 77      | 13      | 4        | 1         | 0         | 0         | 0     |
| SEC    | 68    | 54      | 17      | 1        | 0         | 0         | 0         | 0     |
| **Total** | **178** | **131** | **30** | **5** | **1** | **0** | **0** | **0** |

---

**Distribution Plots**

- Document length histogram  
  ![Document Length Histogram](stats/doc_length_hist.png)

- Summary length histogram  
  ![Summary Length Histogram](stats/summary_length_hist.png)

- Document length ECDF (log scale)  
  ![Document Length ECDF](stats/doc_length_ecdf.png)

---

## ⚖️ Ethics Statement

All documents are public U.S. government regulatory filings obtained via [regulations.gov](https://www.regulations.gov/).  
The dataset contains **no personal or sensitive information**. Redistribution is intended solely for **academic and research purposes**.  

---

## 🔗 Citation

If you use ReguSum in your work, please cite this repository and link to the dataset.

```
@misc{regusum2025,
  author = {Gokhan, Tuba},
  title = {ReguSum: Regulatory Summarization Dataset},
  year = {2025},
  howpublished = {\url{https://github.com/RegNLP/ReguSum}}
}
```
