# recomended_product_restocking_system
Product Sales Forecasting & Restocking System

Project Overview

This project is a product sales analysis and future restocking prediction system built using the Dunnhumby – The Complete Journey dataset.

The system analyzes historical product-category sales and customer purchase data to understand demand patterns and help determine how much stock should be maintained or restocked in the future.

The project includes separate data pipelines for Volatile and Normal product categories because their sales patterns behave differently.

Dataset

Dataset: Dunnhumby – The Complete Journey

The dataset contains information related to:

- Products and product categories
- Customer purchases
- Sales transactions
- Store information
- Product departments
- Historical purchasing behavior

Data Categories

After data analysis, products/categories are divided into two groups:

1. Volatile Products

These products have highly changing or unpredictable sales patterns.

They require a separate data-processing pipeline and forecasting approach because their demand can change significantly over time.

2. Normal Products

These products have more stable and predictable sales patterns.

A separate pipeline is used for these products to process their data and generate appropriate predictions.

Data Pipelines

The project uses two different pipelines:

Raw Dataset
     |
     v
Data Cleaning & Preprocessing
     |
     v
EDA
     |
     +-------------------+
     |                   |
     v                   v
Volatile Products    Normal Products
     |                   |
     v                   v
Volatile Pipeline   Normal Pipeline
     |                   |
     v                   v
Forecasting Model   Forecasting Model
     |                   |
     +---------+---------+
               |
               v
       Restocking Recommendation

Exploratory Data Analysis (EDA)

EDA is performed before model development to understand the dataset and identify important patterns such as:

- Sales trends
- Product-category demand
- Seasonal patterns
- High and low demand periods
- Stable vs. fluctuating products
- Missing or inconsistent data
- Historical purchasing patterns

The results of EDA are used to decide which products/categories belong to the Volatile or Normal category.

Machine Learning Models

Models are applied after EDA and preprocessing.

The model selection can differ between the two pipelines depending on the characteristics of the data.

EDA
 ↓
Identify Sales Pattern
 ↓
Volatile / Normal Classification
 ↓
Separate Pipeline
 ↓
Model Training
 ↓
Future Sales Prediction

User Interface

The project uses CustomTkinter to create a graphical user interface (GUI).

The UI allows the user to interact with the system and view the forecasting and restocking results without directly working with the code.

Possible UI features include:

- Upload/select dataset
- Select product category
- View sales information
- View predicted future demand
- View restocking recommendation
- Display graphs and analysis results

Use Case

The main purpose of the system is to help businesses make better inventory decisions.

The system:

1. Takes historical product-category sales data.
2. Analyzes the sales patterns.
3. Separates products into Volatile and Normal categories.
4. Sends each category through its respective pipeline.
5. Uses trained models to predict future demand.
6. Provides a restocking recommendation based on the predicted demand.

Example

If a product category has increasing predicted demand for the coming weeks, the system can recommend maintaining higher stock levels.

If demand is predicted to remain low or stable, the system can recommend a lower restocking quantity.

Technology Stack

- Python – Main programming language
- Pandas – Data processing
- NumPy – Numerical operations
- Matplotlib / Seaborn – Data visualization
- Scikit-learn – Machine learning
- CustomTkinter – Graphical User Interface
- MySQL (if used) – Database management
- Git – Version control
- GitHub – Source-code repository and collaboration

Version Control

Git and GitHub are used for version control.

Git helps in:

- Tracking changes in the project
- Maintaining different versions
- Managing branches
- Reverting unwanted changes
- Collaborating with team members

GitHub is used to host and manage the project repository.

Project Objective

The objective of this project is to develop a sales forecasting and inventory restocking system that can analyze historical sales data, predict future product demand, and provide useful restocking recommendations.

The use of separate pipelines for Volatile and Normal products makes the system more suitable for products with different sales behaviors.

Expected Output

The final system should provide:

Product Category → Sales Analysis → Demand Prediction → Restocking Recommendation

This can help businesses reduce:

- Over-stocking
- Under-stocking
- Inventory waste
- Missed sales opportunities

and improve overall inventory planning.
