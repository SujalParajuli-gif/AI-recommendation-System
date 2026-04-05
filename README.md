# Personalized Top-N Product Recommendation System

A machine learning-based recommendation system that generates **Top-N product recommendations** from real e-commerce interaction data. This project uses the **Amazon Reviews 2023 Electronics** dataset and compares three recommendation approaches: a **Popularity Baseline**, **Item-Item Collaborative Filtering using cosine similarity**, and **TruncatedSVD** as the main personalized model.

## Project Overview

Online shopping platforms contain a very large number of products, which can make it difficult for users to find items that match their interests. This project addresses that problem by building a recommendation pipeline that learns from **user-item interactions** such as ratings and review activity.

The system is designed to:

- clean and prepare real-world e-commerce data
- build recommendation models using interaction history
- generate ranked Top-N recommendations for a selected user
- compare multiple recommendation approaches fairly
- evaluate ranking quality using standard Top-K metrics

## Main Objectives

- Build an end-to-end recommendation workflow using real product review data
- Compare three recommendation strategies on the same dataset
- Use a **time-aware train/test split** for realistic evaluation
- Recommend only **unseen items** to the user
- Provide a simple **CLI-based interface** for testing recommendations

## Dataset

This project uses the **Amazon Reviews 2023** dataset from the **Electronics** category.

### Data used
- **Review interactions**: `user_id`, `parent_asin`, `rating`, `timestamp`
- **Product metadata**: product title and related descriptive fields

### Final cleaned dataset
After cleaning and filtering, the final dataset used in the system contains:
- **10,991 interactions**
- **2,632 users**
- **3,764 items**

The cleaned dataset is exported as a CSV and then reused consistently for training and evaluation.

## Recommendation Methods

### 1. Popularity Baseline
A non-personalized recommender that ranks items by overall interaction frequency in the training data.

**Why it is used**
- strong baseline for comparison
- helpful for cold-start situations
- simple and fast to implement

### 2. Item-Item Collaborative Filtering
This approach uses **cosine similarity** between items. It recommends products that are similar to the items a user has already interacted with.

**Why it is used**
- more explainable than many black-box approaches
- supports “similar products” style recommendations
- useful when a user already has some interaction history

### 3. TruncatedSVD
This is the main personalized recommendation method. It reduces the user-item interaction matrix into latent factors and reconstructs preference scores for ranking unseen items.

**Why it is used**
- works well with sparse interaction data
- provides personalized ranking
- academically easier to explain and implement clearly in a notebook workflow

## Project Workflow

The implementation is organized into **two notebooks**:

### Notebook 1 — Data Preparation
- load reviews data
- load product metadata
- merge both datasets using `parent_asin`
- clean missing and invalid records
- remove duplicates
- export the cleaned CSV

### Notebook 2 — Recommender System
- load the cleaned CSV
- perform exploratory data analysis (EDA)
- apply a **time-aware train/test split**
- build the user-item interaction matrix
- train all three recommenders
- evaluate them using Top-K metrics
- run a CLI for user-based recommendation output

## Evaluation Metrics

The models are evaluated using **Top-K ranking metrics**:

- **Precision@K** – how many recommended items are relevant
- **Recall@K** – how many relevant items are recovered in the recommendation list
- **NDCG@K** – how well relevant items are ranked near the top

These metrics are used because the goal is not to predict a single label, but to produce a **ranked recommendation list**.

## Key System Design Decisions

### Time-aware split
For each user, the **most recent interaction** is used as the test instance, while earlier interactions are used for training. This makes the evaluation more realistic and reduces data leakage.

### Unseen-item recommendation
Items already present in a user’s training history are removed from the final recommendation list.

### Sparse-data suitability
Because recommendation datasets are typically sparse, the project focuses on methods that can still work effectively when most user-item pairs have no interaction.

## Tools and Technologies

- **Python**
- **Jupyter Notebook**
- **Pandas**
- **SciPy**
- **Matplotlib**
- **scikit-learn**
- **Anaconda Navigator**

## Example Project Structure

```bash
project-root/
│
├── data/
│   ├── reviews.jsonl
│   ├── metadata.jsonl
│   └── cleaned_filtered_reviews_metadata.csv
│
├── notebooks/
│   ├── 01_data_preparation.ipynb
│   └── 02_recommender_system.ipynb
│
├── outputs/
│   ├── charts/
│   ├── evaluation_table.png
│   └── comparison_chart.png
│
├── README.md
└── requirements.txt
```

## Setup Instructions

### 1. Clone the repository
```bash
git clone <your-github-repo-link>
cd <your-project-folder>
```

### 2. Create and activate a virtual environment
```bash
python -m venv venv
```

#### Windows
```bash
venv\Scripts\activate
```

#### macOS / Linux
```bash
source venv/bin/activate
```

### 3. Install dependencies
```bash
pip install -r requirements.txt
```

### 4. Launch Jupyter Notebook
```bash
jupyter notebook
```

### 5. Run the notebooks in order
1. `01_data_preparation.ipynb`
2. `02_recommender_system.ipynb`

## Example Requirements

Create a `requirements.txt` file with packages similar to:

```txt
pandas
numpy
matplotlib
scipy
scikit-learn
jupyter
```

## How to Use

After running the recommender notebook:

1. choose a recommendation method
2. enter a valid `user_id`
3. receive a ranked **Top-N recommendation list**
4. the system maps product IDs to readable product titles
5. invalid input and invalid user IDs are handled safely in the CLI

## Outputs Included in the Project

The project demonstrates:

- cleaned dataset preview
- rating distribution plot
- time-aware split output
- interaction distribution plots
- user-item sparsity heatmap
- item-item similarity output
- TruncatedSVD training and score reconstruction
- evaluation table
- comparison chart
- CLI recommendation results

## Strengths of the Project

- uses real-world e-commerce data
- compares multiple recommendation strategies
- includes both baseline and personalized approaches
- uses realistic evaluation logic
- simple to demonstrate in viva, report, or GitHub portfolio

## Limitations

- cold-start users and items remain challenging
- recommendations are based mainly on interaction data
- the current interface is CLI-based rather than a full web application
- recommendation quality depends on the amount of user history available

## Future Improvements

Possible future enhancements include:

- hybrid recommendation using metadata such as brand, category, and price
- using review text sentiment or browsing behavior as extra signals
- testing across multiple time splits for stronger evaluation
- replacing the CLI with a web-based interface
- improving cold-start handling for new users and new items

## Academic Context

This repository was developed as coursework for an **Artificial Intelligence** module and focuses on building a practical recommendation system using machine learning techniques on real interaction data.

## Author

**Sujal Parajuli**

## License

This project is for **educational and academic use** unless stated otherwise.
