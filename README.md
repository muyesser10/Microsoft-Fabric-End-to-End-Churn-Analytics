
# 🚀 Microsoft-Fabric-End-to-End-Churn-Analytics

![Microsoft Fabric](https://img.shields.io/badge/Microsoft%20Fabric-blue)
![OneLake](https://img.shields.io/badge/OneLake-lightgrey)
![Apache Spark](https://img.shields.io/badge/Apache%20Spark-orange)
![Power BI](https://img.shields.io/badge/Power%20BI-yellow)
![Pyspark](https://img.shields.io/badge/Python-green)
![Delta Lake](https://img.shields.io/badge/Delta%20Lake-brown)

End-to-end churn analytics platform built on **Microsoft Fabric** using **Medallion Lakehouse architecture**, automated pipelines, RFM segmentation, PySpark-based feature engineering, churn modeling, and Power BI dashboard.

---

## 🎯 Executive Summary

This project delivers an **end-to-end customer intelligence platform** built on **Microsoft Fabric** using a **Medallion Lakehouse architecture**.

Transactional e-commerce data is transformed into **actionable business insights** through **structured ingestion pipelines, lakehouse transformations, and customer-level feature engineering**.

By combining **RFM segmentation** with a **machine learning–based churn prediction model**, the platform:

* Identifies high-value customers
* Detects early churn signals
* Quantifies revenue risk

The architecture integrates **data engineering**, **behavioral analytics**, and **predictive modeling** into a unified workflow — from **raw data ingestion** to **executive-level Power BI dashboards**.

---

## 🏗️ Architecture Overview


**Flow:** Raw → Staging → Bronze → Gold → ML → Power BI

<img width="500" height="750" alt="project architecture" src="https://github.com/user-attachments/assets/34879f6e-3fa0-42f4-9dfa-112852791479" />




**Components:**

* **Ingest Pipeline**
* **Process Pipeline**
* **ML Notebook**
* **Master Orchestration Pipeline**
* **Power BI Semantic Model**

---

## 1️⃣ Ingest Pipeline

**Purpose:** Manage data movement from **OneLake Raw → OneLake Staging**

**Data Source:**

* 9 CSV files stored in OneLake (Raw)
* Actively used datasets:

  * `customers.csv`
  * `orders.csv`
  * `order_items.csv`
  * `order_reviews.csv`

**Flow:**

1. **Get Metadata** → Reads all files in Raw
2. **ForEach** → Iterates over files
3. **If Condition** → Filters required datasets
4. **Copy Activity** → Moves selected files to Staging

 Ensures Raw data remains untouched while Staging acts as a controlled processing layer.

<img width="955" height="443" alt="ingestPipeline" src="https://github.com/user-attachments/assets/0f922d38-1ec1-40e5-a1de-4c76323bfee0" />
<img width="954" height="444" alt="1) stagingLakeHouse_raw" src="https://github.com/user-attachments/assets/489a8f2b-89f4-45f7-a83f-2459b708d27a" />
<img width="958" height="444" alt="2) stagingLakehouse_staging" src="https://github.com/user-attachments/assets/ea74917b-09fe-4bb1-b579-e22c108be415" />




---

## 2️⃣ Process Pipeline

**Purpose:** Transform data across **Medallion layers**

### 🔹 Staging → Bronze (Dataflow)

* CSV files are written to **Bronze Lakehouse**
* Stored as **Delta Tables**

<img width="957" height="448" alt="3) bronzeLakehouse" src="https://github.com/user-attachments/assets/3a78b3ea-6321-40fb-8c61-b204e46b20b2" />


### 🔹 Bronze → Gold (Transformation Notebook)

* **Data cleaning and transformation:**

  * Table joins
  * **RFM metric calculation**
  * 90-day behavioral aggregation
  * Churn label generation

**Outputs:**

* `gold_rfm_customer`
* `gold_churn_model_dataset`

### 🔹 ML Notebook

* **Feature engineering** on churn dataset
* **Spark ML model training**
* **Churn probability scoring**

**Final output table:** `gold_churn_customer_score`


<img width="949" height="442" alt="processPipeline" src="https://github.com/user-attachments/assets/1245ea17-b068-4993-a9d3-cf262a67a9b5" />
<img width="953" height="447" alt="4) goldLakehouse" src="https://github.com/user-attachments/assets/7334f41a-ffe7-49bc-976d-8f122fd22d74" />


---

## 3️⃣ Business Logic: RFM & Churn Modeling

### 🔹 RFM Segmentation

* **Recency:** Days since last order
* **Frequency:** Order count
* **Monetary:** Total & average spend

**Enables identification of:**

* High-value customers
* Recently inactive customers
* Potential churn risk segments

**Output table:** `gold_rfm_customer`

---

### 🔹 Churn Definition

* Customer is labeled **churned** if:

  * No purchase for **>120 days**
  * At least **2 historical orders**

> Avoids mislabeling one-time buyers.

---

### 🔹 Churn Prediction

* Trained on **engineered customer-level features**
* Generates **0–1 churn probability score**
* Stored in `gold_churn_customer_score`
* Used in **Power BI** for:

  * Risk segmentation
  * Revenue exposure analysis

---

## 4️⃣ Orchestration

**Master Pipeline** coordinates:

* Ingest Pipeline
* Process Pipeline

> Ensures **end-to-end automation**.

<img width="957" height="446" alt="masterPipeline" src="https://github.com/user-attachments/assets/af6be61b-c1f4-4ac4-a779-e79a816c2097" />


---

## 📊 Power BI Dashboard

* Gold Lakehouse tables connected to **Semantic Model**
* Visualized in **Power BI**

**Dashboard insights:**

* Churn rate per RFM segment
* Churned customers complaint rate
* Churned customers shipment delay rate


<img width="953" height="447" alt="power_bi" src="https://github.com/user-attachments/assets/22b11189-0c0a-4737-9533-070bbb9c176a" />


---

## 🧩 Tech Stack

* **Microsoft Fabric**
* **OneLake**
* **Lakehouse (Delta Tables)**
* **Apache Spark**
* **Spark ML**
* **Power BI**

---

## 📂 Dataset

**Brazilian E-Commerce Public Dataset (Olist)**

* Used for **customer behavior analytics** and **churn modeling simulation**

[Kaggle Link](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce/data)

---

## 🎯 Project Highlights

* Medallion architecture implementation
* Pipeline orchestration
* Feature engineering (behavioral + time-based)
* ML-based churn scoring
* Business intelligence integration

