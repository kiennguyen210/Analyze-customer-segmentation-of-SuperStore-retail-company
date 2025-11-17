# Customer Segmentation For Marketing Campaigns in SuperStore (Global Retail Company) | Python
<img width="900" height="600" alt="Image" src="https://github.com/user-attachments/assets/f26fd9d1-2d88-4dec-a650-d558bae94f47" />

*Applying the RFM model built with Python to segment customers and recommend appropriate marketing campaigns.*

**Author:** Nguyễn Duy Kiên

**Date:** October 2025

**Tools Used:** Python

---

## 📑 Table of Contents  
1. [📌 Background & Overview](#1--background--overview)  
2. [📂 Dataset Description & Data Structure](#2--dataset-description--data-structure)
3. [🔍 Exploratory Data Analysis (EDA)](3--exploratory-data-analysis-eda)
4. [🧮 Data Processing](4--data-processing)
5. [📊 Visulization & Analysis](5--visulization--analysis)
6. [🔎 Insights & Recommendations](6--insights--recommendations)

---

## 1. 📌 Background & Overview 

### 1.1. Objective:
### 📖 What is this project about? What Business Question will it solve?

🎯 Main Business Question

How can SuperStore use RFM segmentation to efficiently categorize customers and design high-impact marketing campaigns for Christmas and New Year?

📘 Project Overview

- This project applies the RFM (Recency – Frequency – Monetary) model to segment customers based on their purchase behavior.
- The goal is to analyze customer value and classify customers into actionable segments for marketing campaigns.
- The dataset comes from SuperStore, a global retail company with a large customer base.
- Because of the large volume of data, the segmentation is implemented with Python, replacing the manual Excel method previously used.
- The analysis includes:
    + Preparing RFM-ready dataset
    + Calculating R, F, M scores (using 31/12/2011 as the reference date for Recency)
    + Applying quintile scoring (1–5 scale)
    + Assigning segments
    + Visualizing segment distributions
    + Giving insights and marketing recommendations

💡 Business Questions this project answers

- ✔️ How can SuperStore segment its entire customer base using RFM to support targeted marketing?
- ✔️ Which customer groups have high value (loyal, big spenders) and which groups have churn risk?
- ✔️ How should Marketing tailor campaigns for each segment to maximize retention, loyalty, and sales uplift?
- ✔️ What is the current distribution of customer value across Recency, Frequency, and Monetary?
- ✔️ Which RFM dimension is most critical for SuperStore’s retail business model?

### 1.2. Who is this project for?  

- ✔️ Marketing Department – to personalize campaigns, allocate budgets, and target high-value or at-risk customers.
- ✔️ Sales Teams – to identify loyal customers and upsell/cross-sell opportunities.
- ✔️ Customer Experience / CRM Teams – to tailor retention and reactivation programs.
- ✔️ Data Analytics Department – to automate segmentation pipelines and maintain scalable customer analytics.
- ✔️ Business Leaders / Executives – to understand customer value distribution and guide strategic planning.

### 1.3. Why RFM? How to apply RFM?

🚩 Why RFM?

RFM is a marketing method that looks at three things: Recency, Frequency, and Monetary value.
- Recency: How long it has been since a customer last bought something.
- Frequency: How many times the customer has made purchases.
- Monetary: How much money the customer has spent in total.

This method helps businesses group and understand their customers based on how recently they buy, how often they buy, and how much they spend. RFM is especially useful for small and medium businesses because it helps them target the right customer groups, increase ROI, lower churn, save marketing cost, and improve customer relationships.

🚩 How does it work?
- In RFM analysis, each customer is given a score for Recency, Frequency, and Monetary value. To do this, the data is usually split into five groups (quintiles) for each factor. 
- After scoring all three metrics using these quintiles, customers are then grouped into segments based on the combination of their R, F, and M scores. This helps businesses easily identify high-value customers, loyal customers, or customers at risk of leaving.

---

## 2. 📂 Dataset Description & Data Structure

### 2.1. Tables Used

The dataset consists of two tables (sheets):
- Sheet 1: E-commerce Retail – Contains transaction-level data, including order details, customer IDs, and purchase information.

|        | InvoiceNo | StockCode |                         Description | Quantity |         InvoiceDate | UnitPrice | CustomerID |        Country |
|-------:|----------:|----------:|------------------------------------:|---------:|--------------------:|----------:|-----------:|---------------:|
|    0   |    536365 |    85123A |  WHITE HANGING HEART T-LIGHT HOLDER |        6 | 2010-12-01 08:26:00 |      2.55 |    17850.0 | United Kingdom |
|    1   |    536365 |     71053 |                 WHITE METAL LANTERN |        6 | 2010-12-01 08:26:00 |      3.39 |    17850.0 | United Kingdom |
|    2   |    536365 |    84406B |      CREAM CUPID HEARTS COAT HANGER |        8 | 2010-12-01 08:26:00 |      2.75 |    17850.0 | United Kingdom |
|    3   |    536365 |    84029G | KNITTED UNION FLAG HOT WATER BOTTLE |        6 | 2010-12-01 08:26:00 |      3.39 |    17850.0 | United Kingdom |
|    4   |    536365 |    84029E |      RED WOOLLY HOTTIE WHITE HEART. |        6 | 2010-12-01 08:26:00 |      3.39 |    17850.0 | United Kingdom |
|   ...  |       ... |       ... |                                 ... |      ... |                 ... |       ... |        ... |            ... |
| 541904 |    581587 |     22613 |         PACK OF 20 SPACEBOY NAPKINS |       12 | 2011-12-09 12:50:00 |      0.85 |    12680.0 |         France |
| 541905 |    581587 |     22899 |         CHILDREN'S APRON DOLLY GIRL |        6 | 2011-12-09 12:50:00 |      2.10 |    12680.0 |         France |
| 541906 |    581587 |     23254 |        CHILDRENS CUTLERY DOLLY GIRL |        4 | 2011-12-09 12:50:00 |      4.15 |    12680.0 |         France |
| 541907 |    581587 |     23255 |     CHILDRENS CUTLERY CIRCUS PARADE |        4 | 2011-12-09 12:50:00 |      4.15 |    12680.0 |         France |
| 541908 |    581587 |     22138 |        BAKING SET 9 PIECE RETROSPOT |        3 | 2011-12-09 12:50:00 |      4.95 |    12680.0 |         France |

- Sheet 2: Segmentation – Stores customer segments along with their RFM scores.

|        Segment        |                                                        RFM Score                                                       |
|:---------------------:|:----------------------------------------------------------------------------------------------------------------------:|
| Champions             | 555, 554, 544, 545, 454, 455, 445                                                                                      |
| Loyal                 | 543, 444, 435, 355, 354, 345, 344, 335                                                                                 |
| Potential Loyalist    | 553, 551, 552, 541, 542, 533, 532, 531, 452, 451, 442, 441, 431, 453, 433, 432, 423, 353, 352, 351, 342, 341, 333, 323 |
| New Customers         | 512, 511, 422, 421, 412, 411, 311                                                                                      |
| Promising             | 525, 524, 523, 522, 521, 515, 514, 513, 425, 424, 413, 414, 415, 315, 314, 313                                         |
| Need Attention        | 535, 534, 443, 434, 343, 334, 325, 324                                                                                 |
| About To Sleep        | 331, 321, 312, 221, 213, 231, 241, 251                                                                                 |
| At Risk               | 255, 254, 245, 244, 253, 252, 243, 242, 235, 234, 225, 224, 153, 152, 145, 143, 142, 135, 134, 133, 125, 124           |
| Cannot Lose Them      | 155, 154, 144, 214, 215, 115, 114, 113                                                                                 |
| Hibernating Customers | 332, 322, 233, 232, 223, 222, 132, 123, 122, 212, 211                                                                  |
| Lost Customers        | 111, 112, 121, 131, 141, 151                                                                                           |

### 2.2. Table Schema & Data Snapshot

📌 Sheet 1: E-commerce Retail

| Column Name |    Data Type   |                                                Description                                                |
|:-----------:|:--------------:|:---------------------------------------------------------------------------------------------------------:|
| InvoiceNo   | object         | Unique invoice number for each transaction (6-digit). If it starts with 'C', it indicates a cancellation. |
| StockCode   | object         | Unique product (item) code (5-digit).                                                                     |
| Description | object         | Product (item) name.                                                                                      |
| Quantity    | int64          | The number of units purchased per transaction.                                                            |
| InvoiceDate | datetime64[ns] | Date and time when the transaction occurred.                                                              |
| UnitPrice   | float64        | Price per unit of the product in sterling.                                                                |
| CustomerID  | float64        | Unique 5-digit identifier for each customer.                                                              |
| Country     | object         | Name of the country where the customer resides.                                                           |

📌 Sheet 2: Segmentation

| Column Name |          Description          |
|:-----------:|:-----------------------------:|
| Segment     | Segment Name                  |
| RFM Score   | List of score in that Segment |

## 3. 🔍 Exploratory Data Analysis (EDA)

## 4. 🧮 Data Processing

## 5. 📊 Visulization & Analysis

## 6. 🔎 Insights & Recommendations
