# 🚗 ParkWise: Smart Real-Time Pricing for Urban Parking

## 📘 Project Overview

**ParkWise** is a data-driven smart pricing system designed to improve the efficiency of urban parking lots. Developed during the **Summer Analytics 2025** program at **IIT Guwahati**, the project addresses issues like congestion and underutilization by dynamically adjusting parking fees in real time.

It consumes live streaming data from multiple parking areas and considers various parameters such as occupancy, queue length, traffic, special events, and vehicle type. The system runs **three distinct pricing strategies**, from a basic model to a competitive approach, and visualizes price updates using interactive dashboards.

---

## 🎯 Project Goals

- Build a dynamic pricing engine for multiple parking locations.
- Design pricing algorithms from scratch using core Python libraries.
- Implement real-time price computation using a streaming framework.
- Create interactive dashboards to monitor and explain pricing changes.

---

## 🛠️ Tech Stack

This project utilizes a combination of Python tools for data processing, machine learning, and visualization:

- **Python**: Core programming language.
- **NumPy**: For numerical computations and implementing algorithms like linear regression.
- **Pandas**: Used for cleaning and managing the historical dataset.
- **Pathway**: High-performance Python library for real-time stream processing.
- **Bokeh**: For rendering live, interactive plots in the browser.
- **Panel**: Used to build and serve dashboards containing Bokeh plots.
- **Google Colab**: Development environment for writing and testing code.

---

## 📐 Architecture Diagram

```
 graph TD  
        A\[Raw Parking Data Stream\] \--\> B(Pathway Data Ingestion);  
        B \--\> C{Feature Engineering};  
        C \--\> D\[Dynamic Pricing Logic\];  
        D \-- Predicted Prices \--\> E\[Real-time Price Output\];  
        C \-- Occupancy, Queue, Traffic \--\> F\[Utilization & Demand Analysis\];  
        E \--\> G(Bokeh Visualizations);  
        F \--\> G;  
        G \--\> H\[Interactive Dashboard\];

        subgraph Pricing Engine  
            C  
            D  
            E  
            F  
        end

        style A fill:\#f9f,stroke:\#333,stroke-width:2px  
        style B fill:\#bbf,stroke:\#333,stroke-width:2px  
        style C fill:\#ccf,stroke:\#333,stroke-width:2px  
        style D fill:\#ddf,stroke:\#333,stroke-width:2px  
        style E fill:\#eef,stroke:\#333,stroke-width:2px  
        style F fill:\#ffc,stroke:\#333,stroke-width:2px  
        style G fill:\#cfc,stroke:\#333,stroke-width:2px  
        style H fill:\#fcc,stroke:\#333,stroke-width:2px
```

---

## ⚙️ System Workflow

### 1. Data Preprocessing
- Initial data (dataset.csv) includes features like occupancy, traffic, vehicle type, and more.
- The data is cleaned and preprocessed using Pandas and NumPy:
  - Timestamps are created from date and time columns.
  - Categorical values are encoded numerically.
  - Features are normalized to a [0,1] range.
  - A Demand_Proxy is calculated to train the pricing model.

### 2. Offline Model Training
- A linear regression model (Model 2) is trained using NumPy’s Normal Equation method.
- It learns coefficients based on features like occupancy, queue length, traffic, etc.
- These coefficients are later used in the live pricing pipeline.

### 3. Simulated Data Streaming with Pathway
- The cleaned dataset is exported as parking_data_stream.csv.
- Pathway simulates live data input using pw.demo.replay_csv.
- A schema is defined to structure incoming data.

### 4. Real-time Pricing Engine
- Streaming records are processed through three pricing models:
  - **Model 1**: Linear pricing based on occupancy.
  - **Model 2**: Demand-based pricing using learned coefficients.
  - **Model 3**: Competitive pricing adjusted by occupancy and competitor benchmarks.
- All models maintain price bounds to avoid extreme values.
- Results are combined into a unified table (combined_prices).

### 5. Live Dashboard Visualization
- Bokeh plots show price updates for each parking lot in real time.
- Panel organizes and displays these plots on an interactive dashboard.
- Users can observe and compare price behavior from each model.

### 6. Pipeline Execution
- The pipeline runs continuously using pw.run(), processing new data as it streams in and updating the visual interface in real time.

---

## **📁 Repository Contents**

    .  
    ├── Parky.ipynb           \# Main Jupyter Notebook with Pathway pipeline and Bokeh setup  
    ├── README.md                 \# This README file  
    ├── dataset.csv               \# The raw dataset used for simulation  
    ├── parking\_data\_stream.csv   \# (Optional) Simulated real-time data stream  
