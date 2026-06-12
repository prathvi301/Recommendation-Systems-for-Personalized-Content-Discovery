# Recommendation Systems for Personalized Content Discovery

> Netflix Prize Dataset | Collaborative Filtering | Matrix Factorization | Personalized Recommendations

## Project Overview

This project develops and evaluates large-scale recommendation systems using the Netflix Prize Dataset, one of the most influential datasets in recommender systems research.

The objective is to learn user preferences from historical movie ratings and generate personalized recommendations for unseen content.

The project was developed as part of a Machine Learning and Recommendation Systems challenge focused on recommendation quality, ranking performance, scalability, and practical deployment considerations.

---

## Problem Statement

Build a recommendation engine capable of:

- Learning user preferences from historical interactions
- Predicting ratings for unseen movies
- Generating Top-K personalized recommendations
- Comparing multiple recommendation approaches
- Evaluating both rating prediction accuracy and ranking quality

---

## Dataset

Netflix Prize Dataset

Dataset Source:

https://www.kaggle.com/datasets/netflix-inc/netflix-prize-data

### Original Dataset Statistics

| Metric | Value |
|----------|----------|
| Ratings | 100,480,507 |
| Users | 480,189 |
| Movies | 17,770 |
| Rating Scale | 1–5 Stars |

### Note

Due to GitHub storage limitations, the raw dataset and processed parquet files are **not included** in this repository.

Please download the dataset from Kaggle and place it inside:

```text
dataset/
```

---

## Dataset Challenges

The Netflix dataset presents several real-world recommendation challenges:

- Extremely sparse user-item matrix
- Long-tail user activity distribution
- Popularity bias
- Cold-start users
- Large-scale collaborative filtering

---

## Exploratory Data Analysis

The project includes detailed EDA covering:

- Rating distribution analysis
- User activity patterns
- Movie popularity distribution
- Data sparsity analysis
- Long-tail behavior
- Recommendation system implications

### Key Findings

- User activity follows a strong power-law distribution.
- Movie popularity is highly concentrated among a small subset of movies.
- Ratings are positively skewed toward higher values.
- The interaction matrix is extremely sparse.
- Collaborative filtering is highly suitable for this dataset.

---

## Recommendation Models

### 1. Baseline Model

Bias-corrected rating prediction model:

Rating Prediction =

```text
Global Mean
+ User Bias
+ Item Bias
```

Used as a benchmark for comparison.

---

### 2. Singular Value Decomposition (SVD)

Matrix factorization model that learns latent user and movie representations.

Configuration:

```python
n_factors = 100
n_epochs = 20
lr_all = 0.005
reg_all = 0.02
```

Advantages:

- Captures hidden preference patterns
- Scales well
- Strong predictive performance

---

### 3. Item-Based Collaborative Filtering (Item-KNN)

Neighborhood-based recommender using item-item similarities.

Configuration:

```python
k = 20
similarity = cosine
```

Because the full item-item similarity matrix exceeds memory limits on an 8 GB machine, KNN was trained on the top 2,000 most-rated movies.

Advantages:

- Highly interpretable
- Explainable recommendations
- Strong ranking performance

---

## Evaluation Methodology

### Train-Test Split

The provided Netflix probe set was used as the evaluation set.

### Relevant Item Definition

A movie is considered relevant if:

```text
Actual Rating >= 3.5
```

### Metrics

Mandatory Metrics:

- RMSE
- MAP@10

Additional Metrics:

- MAE
- Precision@10
- Recall@10

---

## Final Results

| Model | RMSE | MAE | MAP@10 | P@10 | R@10 |
|---------|---------|---------|---------|---------|---------|
| Baseline | 0.9728 | 0.7640 | 0.0348 | 0.0186 | 0.0806 |
| SVD | 0.9141 | 0.7063 | 0.0517 | 0.0287 | 0.1292 |
| Item-KNN | 0.9368 | 0.7215 | 0.0529 | 0.0307 | 0.1415 |

### Key Insights

- SVD achieved the best rating prediction accuracy.
- SVD improved RMSE by approximately 6% over the baseline.
- SVD improved MAP@10 by approximately 49% over the baseline.
- Item-KNN achieved the highest ranking metrics in sampled evaluation.
- KNN provides strong explainability and recommendation transparency.

---

## Recommendation Generation

The system generates:

- Personalized Top-10 recommendations
- Explainable Item-KNN recommendations
- Cold-start recommendations
- Success case analysis
- Failure case analysis

### Example Explanation

```text
Recommended: Movie C

Because you liked:

- Movie A (5★)
- Movie B (5★)
- Movie D (4★)
```

---

## Cold Start Strategy

For new users with little or no interaction history:

- Popularity-based recommendations are used
- Most highly rated movies are recommended
- Serves as a fallback until sufficient user history is collected

---

## Project Structure

```text
Recommendation-Systems-for-Personalized-Content-Discovery/

│
├── notebook.ipynb
│
├── report/
│   └── Technical_Report.pdf
│
├── presentation/
│   └── Presentation.pdf
│
├── models/
│   ├── baseline.pkl
│   ├── svd.pkl
│   ├── knn.pkl
│   └── results_fixed.csv
│
├── outputs/
│   ├── figures/
│   └── recs/
│
├── requirements.txt
│
├── .gitignore
│
└── README.md
```

---

## Installation

Clone the repository:

```bash
git clone <your-repository-url>
cd Recommendation-Systems-for-Personalized-Content-Discovery
```

Install dependencies:

```bash
pip install -r requirements.txt
```

---

## Running the Project

### Step 1

Download the Netflix Prize Dataset from Kaggle.

### Step 2

Place the dataset inside:

```text
dataset/
```

### Step 3

Open and run:

```bash
jupyter notebook notebook.ipynb
```

The notebook performs:

- Data preprocessing
- Exploratory Data Analysis
- Model training
- Evaluation
- Recommendation generation

---

## Technical Report

Detailed methodology, experiments, analysis, and results are available in:

```text
report/Technical_Report.pdf
```

---

## Presentation

Project presentation slides are available in:

```text
presentation/Presentation.pdf
```

---

## Future Improvements

Possible extensions include:

- SVD++
- Alternating Least Squares (ALS)
- Neural Collaborative Filtering
- Hybrid Recommendation Systems
- Temporal Recommendation Models
- Content-Based Features
- Deep Learning Approaches

---

## Author

**Prathvi Paliwal**


---

## License

This repository is intended for educational and academic purposes only.

Netflix Prize Dataset ownership remains with Netflix and the dataset providers.
