Recommended Product Restocking System — Alpha 1

<p align="center">
  <img src="https://img.shields.io/badge/Version-Alpha%201-orange?style=for-the-badge" alt="Alpha 1" />
  <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python" />
  <img src="https://img.shields.io/badge/Machine%20Learning-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white" alt="Machine Learning" />
  <img src="https://img.shields.io/badge/CustomTkinter-4C4A48?style=for-the-badge&logo=python&logoColor=white" alt="CustomTkinter" />
</p>«Alpha 1 — Proof of Concept

An exploratory retail analytics and product relationship discovery system that uses anonymous receipt-level transaction data to identify purchasing patterns, product associations, spending behaviour, and hidden relationships between products. This version establishes the analytical foundation for a future machine learning-assisted inventory forecasting and replenishment system.»

---

1. Project Overview

The Recommended Product Restocking System aims to develop an intelligent retail inventory and replenishment platform using transaction data, machine learning, and data analytics.

The first development stage, Alpha 1, focuses on establishing a proof of concept using the receipt-level information available in the Dunnhumby The Complete Journey dataset.

Rather than immediately attempting to predict inventory requirements, Alpha 1 investigates how products relate to one another through purchasing behaviour.

The system explores questions such as:

- Which products are regularly purchased together?
- Which products have strong purchasing associations?
- Do product combinations change according to the total spending of a receipt?
- Can products be grouped according to similar purchasing behaviour?
- Can dimensionality reduction reveal hidden relationships between products?
- Are there unusual receipt compositions or unexpected purchasing patterns?
- Can product relationships be represented and explored through interactive visualizations?

The initial version deliberately limits its input data to a small collection of receipt-derived fields. It does not depend on customer identities, demographics, or personal information.

The long-term objective is to extend these analytical capabilities into an inventory management system that records stock movements, predicts future demand, manages FIFO inventory, and generates intelligent product replenishment recommendations.

---

2. Alpha 1 — Dataset Scope

Dataset

Dunnhumby — The Complete Journey

The dataset provides historical retail transaction records, which will be used as the foundation for developing and testing the initial analytical components.

For Alpha 1, only the following four logical fields are used.

Field| Description| Source / Processing
"BASKET_ID"| Unique receipt or basket identifier| Dunnhumby transaction data
"PRODUCT_ID"| Identifier of the purchased product| Dunnhumby transaction data
"ITEM_LINE_VALUE"| Monetary value associated with the purchased product line| Derived from "SALES_VALUE"
"RECEIPT_TOTAL"| Total value of the products within a receipt| Calculated by aggregating product-line values using "BASKET_ID"

Data interpretation:

- "BASKET_ID" identifies which receipt a purchased product belongs to.
- "PRODUCT_ID" identifies the purchased product.
- "ITEM_LINE_VALUE" represents the monetary value associated with that product's transaction line. It should not automatically be interpreted as a per-unit price.
- "RECEIPT_TOTAL" is calculated by summing the included product-line values belonging to the same basket.

The exact customer-paid receipt total may differ from this calculated value because the Dunnhumby "SALES_VALUE" field represents the amount received by the retailer and has its own discount-related semantics.

The Alpha 1 implementation intentionally excludes additional transaction fields, even where they exist in the original dataset.

Explicitly Excluded Data

The following information will not be used as model inputs in Alpha 1:

- Household or customer identifiers.
- Customer demographics.
- Customer age, income, marital status, or household composition.
- Transaction dates and timestamps.
- Product purchase quantities.
- Store identifiers.
- Coupon and discount information.
- Promotional campaign information.
- External customer profiles or psychographic information.

Important limitation: Because this version does not use purchase quantities or temporal information, it cannot reliably perform unit-level demand forecasting, time-series forecasting, seasonal analysis, or actual inventory replenishment calculations.

---

3. Alpha 1 — Core Features

3.1 Market Basket Analysis

The system will investigate relationships between products that appear together in individual receipts.

It will use association rule mining to discover frequently co-purchased products.

Potential algorithms:

- Apriori
- FP-Growth
- Eclat

Association mining will use three primary statistical measures:

Metric| Purpose
Support| Measures how frequently a product combination occurs across receipts.
Confidence| Measures how frequently another product appears when a particular product is present.
Lift| Measures the strength of an association relative to the products' independent occurrence frequencies.

Potential applications:

- Identifying frequently purchased product combinations.
- Discovering complementary product relationships.
- Identifying products suitable for bundle recommendations.
- Finding unexpectedly strong product associations.
- Comparing the relationships between individual products.

The results represent purchasing associations, not proven causal relationships or confirmed product substitutes.

3.2 Receipt Spending Segmentation

Receipts will be grouped according to their calculated total spending.

The system will investigate purchasing behaviour across different spending segments.

Potential segmentation approaches:

- Median-based segmentation.
- Quartile-based segmentation.
- Spending quantiles.
- K-Means clustering of receipt-level numerical features.

Potential analytical outputs:

- Low-, medium-, and high-spending receipt groups.
- Product occurrence within each spending segment.
- Frequently purchased combinations by spending segment.
- Average number of unique products per receipt.
- Product-line contribution to receipt spending.
- Differences in purchasing associations across spending segments.

This allows the system to investigate whether certain product combinations are more common in lower-value or higher-value receipts.

3.3 Product Behavioural Similarity

Products will be represented according to the receipts in which they appear.

A product-receipt matrix will be constructed using the available transaction records.

For example:

Product| Receipt 1| Receipt 2| Receipt 3| Receipt 4
Product A| 1| 1| 0| 1
Product B| 1| 1| 0| 0
Product C| 0| 0| 1| 1
Product D| 0| 0| 1| 1

A value of "1" indicates that a product appeared in the corresponding receipt.

This representation allows the system to compare products according to their purchasing patterns.

Potential applications:

- Product co-occurrence analysis.
- Behavioural product similarity.
- Product grouping based on receipt appearances.
- Product relationship matrix generation.

These groupings describe behavioural similarity, not necessarily product-category or functional similarity.

3.4 Dimensionality Reduction and Visualization

The project will investigate dimensionality reduction to visualize relationships between products.

Potential techniques:

- Principal Component Analysis (PCA).
- Truncated Singular Value Decomposition (Truncated SVD).

The product-receipt matrix will be transformed into a lower-dimensional representation.

The resulting projections can be used to visualize products according to their purchasing behaviour.

Potential visualizations:

- Two-dimensional product similarity plots.
- Three-dimensional product relationship plots.
- Product clustering visualizations.
- Behavioural group distributions.
- Spending-segment comparisons.

The system may experiment with clustering algorithms on the reduced representations:

- K-Means.
- DBSCAN.
- HDBSCAN.
- Agglomerative Clustering.

PCA and other dimensionality reduction methods are exploratory tools. Proximity in a reduced visualization does not by itself establish a strong product association.

3.5 Product Relationship Network

The system will investigate representing products as an interconnected graph.

In this representation:

- Each node represents a product.
- Each edge represents a purchasing association.
- Edge weights represent the strength of the relationship.

Potential graph analytics include:

- Identifying highly connected products.
- Discovering product communities.
- Identifying products that connect different purchasing groups.
- Exploring unexpected product associations.
- Visualizing purchasing relationships.

Potential algorithms include Louvain community detection and other graph clustering techniques.

3.6 Unusual Purchasing Pattern Discovery

Alpha 1 will also explore statistical techniques for identifying unusual receipt compositions and product relationships.

Potential investigations include:

- Receipts with unusually high calculated totals.
- Unusual combinations of products.
- Rare product combinations with unexpectedly strong associations.
- Products with unusual co-occurrence profiles.
- Differences in purchasing patterns across spending segments.

Potential techniques:

- Isolation Forest.
- Statistical anomaly detection.
- DBSCAN.
- Association rule analysis.

These capabilities will initially be exploratory and will depend on dataset size, quality, and the validation of detected patterns.

---

4. Proposed Analytical Pipeline

The Alpha 1 pipeline is designed around receipt-level information.

graph TD
    A["Dunnhumby Transaction Data"] --> B["Select Four Approved Fields"]
    B --> C["Data Cleaning and Validation"]
    C --> D["Receipt-Level Aggregation"]
    D --> E["Receipt Spending Analysis"]
    D --> F["Product-Receipt Matrix"]
    E --> G["Spending Segmentation"]
    F --> H["Market Basket Analysis"]
    F --> I["Product Similarity Analysis"]
    I --> J["PCA / Truncated SVD"]
    I --> K["Product Relationship Graph"]
    G --> H
    H --> L["Analytical Results"]
    J --> L
    K --> L
    L --> M["Visualizations and Desktop Dashboard"]

The processing stages are:

1. Dataset Selection: Load the Dunnhumby transaction records.
2. Field Restriction: Retain only the four approved logical fields.
3. Data Cleaning: Handle missing product identifiers, invalid monetary values, and duplicate transaction lines.
4. Receipt Aggregation: Group products using "BASKET_ID" and calculate receipt-level totals.
5. Feature Construction: Generate product-presence matrices, receipt spending features, and product relationship measures.
6. Analytical Processing: Apply association mining, clustering, dimensionality reduction, and anomaly detection.
7. Visualization: Present the discovered patterns through charts, product relationship graphs, and interactive analytical views.

---

5. Desktop Interface

The application will use Python and CustomTkinter to provide a desktop interface for interacting with the analytical system.

The proposed interface will focus on:

- Receipt-level spending analysis.
- Product association exploration.
- Product relationship visualizations.
- Spending-segment comparisons.
- PCA and dimensionality reduction plots.
- Product clustering results.
- Unusual purchasing pattern reports.

The objective is to make analytical discoveries understandable and useful rather than simply presenting raw machine learning outputs.

---

6. Technology Stack

The following technologies are proposed for the Alpha 1 proof of concept.

Category| Technology
Programming Language| Python
Desktop Interface| CustomTkinter
Data Processing| Pandas, NumPy
Machine Learning| Scikit-learn
Association Rule Mining| MLxtend
Dimensionality Reduction| Scikit-learn
Clustering| Scikit-learn
Graph Analysis| NetworkX
Data Visualization| Matplotlib / Plotly
Dataset| Dunnhumby The Complete Journey

The selection of individual algorithms and libraries may evolve as the proof of concept is evaluated.

---

7. Privacy Considerations

Alpha 1 follows a receipt-level, privacy-conscious analytical approach.

The system does not require customer names, addresses, demographics, or individual customer profiles.

All behavioural analysis is performed using receipt identifiers and product-level transaction information.

The system focuses on aggregate purchasing patterns rather than identifying individual customers.

No customer-level profiling or demographic-based segmentation is part of the Alpha 1 scope.

---

8. Known Limitations of Alpha 1

Alpha 1 is an analytical proof of concept, not a complete inventory replenishment system.

The restricted dataset imposes the following limitations:

Limitation| Consequence
No quantity information| Cannot reliably forecast units sold.
No transaction timestamps| Cannot perform temporal or seasonal demand forecasting.
No historical inventory records| Cannot identify actual stockout events.
No batch information| Cannot implement batch-level FIFO tracking.
No expiry dates| Cannot calculate product expiry risk.
No supplier information| Cannot calculate supplier lead-time requirements.
No verified product taxonomy| Cannot reliably identify functional product categories or substitutes.
No promotion or discount information| Cannot isolate promotional effects on purchasing behaviour.

In particular, product co-occurrence must not be interpreted as product substitutability. Identifying substitutes requires additional product classification, availability, and temporal purchasing evidence.

---

9. Future Development Roadmap

Alpha 1 establishes the foundation for expanding the proof of concept into a complete inventory intelligence platform.

Future versions will introduce additional data collection through the software itself.

Alpha 2 — Product Intelligence and Data Infrastructure

Potential additions:

- Centralized product catalogue.
- Product name normalization.
- Brand and product-type classification.
- Human-assisted product taxonomy.
- Semantic product similarity.
- Product substitution analysis.
- Database-backed transaction storage.
- Receipt timestamp recording.

Beta — Digital Inventory Management

Potential additions:

- Digital inventory ledger.
- Stock purchase and sales tracking.
- Quantity-level inventory records.
- Batch-level stock tracking.
- FIFO inventory management.
- Expiry and damage tracking.
- Supplier and lead-time records.
- Historical inventory movement analysis.

Future ML Development — Predictive Intelligence

Potential additions:

- Global product demand forecasting.
- Nonlinear demand modelling.
- Intermittent demand forecasting.
- LightGBM and XGBoost experimentation.
- Demand uncertainty estimation.
- Stockout risk prediction.
- Expiry risk prediction.
- Cross-product demand relationships.
- Model evaluation and retraining.

Future Optimization Development — Intelligent Replenishment

Potential additions:

- Safety stock calculation.
- Reorder point calculation.
- Inventory position estimation.
- Recommended purchase quantities.
- Lead-time-aware replenishment.
- Expiry-aware purchasing recommendations.
- Inventory cost and wastage analysis.
- What-if inventory simulations.

These are proposed development directions, not capabilities claimed to be implemented in Alpha 1.

---

10. Long-Term Project Objective

The long-term objective is to develop an intelligent retail inventory management platform that combines:

1. Receipt-level purchasing analytics.
2. Product relationship discovery.
3. Product classification and normalization.
4. Historical demand analysis.
5. Machine learning-based demand forecasting.
6. FIFO inventory management.
7. Inventory optimization.
8. Automated replenishment recommendations.

The system will progressively learn from the data generated through its own inventory management operations.

Rather than relying exclusively on a predefined product classification or a fixed forecasting algorithm, the architecture will allow different analytical and machine learning approaches to be tested and evaluated.

The ultimate goal is to minimize unnecessary inventory accumulation, reduce product wastage, prevent stockouts, and improve replenishment decisions through data-driven analysis.

---

11. Installation and Usage

Prerequisites

- Python 3.x
- Git
- Required Python dependencies

Setup

1. Clone the repository:

git clone <repository-url>
cd recomended_product_restocking_system

2. Create a virtual environment:

python -m venv venv

3. Activate the environment:

# Linux / macOS
source venv/bin/activate

# Windows
venv\Scripts\activate

4. Install dependencies:

pip install -r requirements.txt

5. Run the application using the project's configured entry point.

---

12. Project Structure

Proposed organizational structure:

recomended_product_restocking_system/
│
├── data/
│   ├── raw/                  # Original Dunnhumby data
│   └── processed/            # Restricted and cleaned data
│
├── src/
│   ├── preprocessing/        # Data cleaning and aggregation
│   ├── basket_analysis/      # Association rule mining
│   ├── clustering/           # Product and receipt clustering
│   ├── dimensionality/       # PCA and Truncated SVD
│   ├── graph_analysis/       # Product relationship networks
│   └── anomaly_detection/    # Unusual pattern discovery
│
├── models/                   # Experimental model artifacts
│
├── ui/                       # CustomTkinter components
│
├── visualizations/            # Analytical plotting components
│
├── requirements.txt
├── main.py
└── README.md

---

13. Acknowledgements

Dunnhumby — For providing The Complete Journey, the foundational retail transaction dataset used in developing and evaluating the Alpha 1 proof of concept.

Dataset source: https://www.dunnhumby.com/source-files/

---

Project Status: Alpha 1 — Proof of Concept

The current development stage focuses on discovering purchasing relationships and extracting meaningful retail insights from restricted receipt-level transaction data. Predictive inventory management and automated replenishment remain part of the project's future development roadmap.