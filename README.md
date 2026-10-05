# 🛒 Supermarket Customer Behavior Analysis & Recommendation Using Machine Learning

This project focuses on analysing customer shopping behaviour in a supermarket dataset, performing customer segmentation using machine learning, and building and evaluating different product recommendation approaches.

---

## 📊 Data Scale & Summary

The dataset used in this project contains:

* **Total Transactions:** `527,226`
* **Unique Customers:** `5,000`
* **Unique Invoices/Visits:** `68,034`
* **Unique Products:** `50`
* **Product Categories:** `10`
* **Time Period:** January 2025 to December 2025

The dataset combines customer demographics, transaction details, product information, pricing, discounts, and shopping-time features.

---

## 📌 Table of Contents

1. [Project Overview](#-project-overview)
2. [Dataset Description](#-dataset-description)
3. [Project Workflow](#-project-workflow)

   * [Exploratory Data Analysis](#exploratory-data-analysis)
   * [Customer Segmentation](#customer-segmentation)
   * [Recommendation System](#recommendation-system)
4. [Model Performance](#-model-performance)
5. [Business Insights](#-business-insights)
6. [Technologies Used](#-technologies-used)
7. [How to Run](#-how-to-run)
8. [Conclusion](#-conclusion)

---

## 🎯 Project Overview

The main objectives of the project are to:

* Analyse customer purchasing behaviour and shopping patterns.
* Identify customer groups with similar purchasing behaviour.
* Build product recommendation models using customer purchase history.
* Compare different recommendation approaches using ranking-based evaluation metrics.
* Extract useful business insights from customer and transaction data.

---

## 📋 Dataset Description

The dataset `smart_supermarket_customer_behavior.csv` contains customer, transaction, product, temporal, and marketing-related information.

### Customer Information

* `customer_id` – Unique customer identifier
* `age` – Customer age
* `gender` – Customer gender
* `monthly_income` – Monthly income
* `household_size` – Household size

### Transaction Information

* `invoice_no` – Invoice identifier
* `visit_number` – Customer visit number
* `purchase_date` – Date of purchase
* `quantity` – Number of items purchased
* `total_amount` – Total transaction amount

### Product Information

* `product_category` – Category of the product
* `product` – Product identifier/name
* `original_unit_price` – Original product price
* `discount_pct` – Discount percentage
* `unit_price` – Final unit price

### Temporal Information

* `month` – Month of purchase
* `day_of_week` – Day of purchase
* `purchase_hour` – Hour of purchase

### Marketing / Segment Information

* `used_discount` – Discount usage indicator
* `true_segment` – Existing customer segment label used for validation

---

## 🛠️ Project Workflow

### Exploratory Data Analysis

The dataset was explored to understand its structure and customer behaviour.

Key analysis included:

* Dataset shape, data types, missing values, and duplicates
* Product-category transaction volumes
* Customer purchasing frequency
* Shopping-hour patterns
* Discount usage
* Spending and purchase behaviour

**Personal Care** and **Dairy** were among the highest-volume product categories.

---

### Customer Segmentation

Customer-level behavioural features were created to represent purchasing patterns:

* `spend_per_visit`
* `items_per_visit`
* `spend_per_item`
* `spend_to_income_ratio`

The following techniques were used:

1. **StandardScaler** for feature scaling
2. **K-Means Clustering** for customer segmentation
3. **Elbow Method** and **Silhouette Score** for selecting the number of clusters
4. **PCA** for visualising customer segments in two dimensions
5. **Adjusted Rand Index (ARI)** for comparison with the provided `true_segment` labels

The final clustering solution used **3 customer segments**, with an ARI score of approximately **0.4778**.

---

### Recommendation System

Four recommendation approaches were implemented and evaluated using a **time-based train/test split**, where the customer's latest invoice/visit was held out for testing.

#### V1 - Item-Based Collaborative Filtering

A customer-product interaction matrix was created and **Cosine Similarity** was used to identify similar products based on purchase behaviour.

#### V2 - Weighted Item Similarity

V1 was extended by weighting recommendations according to the customer's relative spending on previously purchased products.

#### V3 - Hybrid Recommender

The hybrid model combined:

* **70%** personalized weighted similarity
* **30%** normalized global product popularity

#### Popularity Baseline

The baseline recommended the most frequently purchased products across the dataset.

---

## 📈 Model Performance

Recommendation performance was evaluated using **Precision@K** and **Recall@K** for `K = 5` and `K = 10`.

| Recommendation Approach  | Precision@5 |   Recall@5 | Precision@10 |  Recall@10 |
| ------------------------ | ----------: | ---------: | -----------: | ---------: |
| V1 - Item Similarity     |      0.0564 |     0.0412 |       0.0459 |     0.0656 |
| V2 - Weighted Similarity |      0.0559 |     0.0405 |       0.0461 |     0.0655 |
| V3 - Hybrid (Sim + Pop)  |      0.0537 |     0.0382 |       0.0455 |     0.0646 |
| **Popularity Baseline**  |  **0.2515** | **0.1754** |   **0.2319** | **0.3126** |

### Key Observation

The **Popularity Baseline** performed substantially better than the personalized recommendation approaches on this evaluation setup.

This suggests that frequently purchased products provide a strong baseline for recommendation in this supermarket dataset, particularly for commonly purchased everyday products.

---

## 💡 Business Insights

The K-Means clustering produced three broad customer behaviour groups:

### Cluster 0 - High-Value Shoppers

Customers with higher spending and larger basket sizes.

**Possible strategy:** premium loyalty rewards and personalised offers.

### Cluster 1 - Frequent Budget Shoppers

Customers with higher visit frequency but relatively smaller transactions.

**Possible strategy:** bundle offers, quantity discounts, and promotions on frequently purchased products.

### Cluster 2 - Premium Shoppers

Customers with higher income and more selective purchasing patterns.

**Possible strategy:** personalised recommendations and category-specific offers.

These segments can be used as a starting point for targeted customer-engagement strategies.

---

## 💻 Technologies Used

* **Python 3**
* **Pandas**
* **NumPy**
* **Matplotlib**
* **Seaborn**
* **Scikit-learn**

  * K-Means
  * PCA
  * StandardScaler
  * Cosine Similarity
  * Silhouette Score
  * Adjusted Rand Index

---

## 🚀 How to Run

Clone the repository:

```bash
git clone https://github.com/your-username/smart-supermarket-analysis.git
cd smart-supermarket-analysis
```

Install the required libraries:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn
```

Open the notebook in **Google Colab or Jupyter Notebook** and run the cells sequentially.

---

## 📌 Conclusion

This project combines **exploratory data analysis, customer segmentation, clustering, and recommendation-system evaluation** to study supermarket customer behaviour.

The analysis identified three customer segments, while the recommendation experiments showed that the simple **Popularity Baseline** performed better than the personalised approaches on the selected evaluation setup. This highlights the importance of comparing advanced recommendation methods against strong and simple baselines.
