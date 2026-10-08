# ⚡ U.S. Data Centers: Footprint, Pipeline & Risk Analysis

An end-to-end data analytics and geospatial study evaluating **1,621 U.S. data center facilities**. This project examines spatial clustering, speculative development pipelines, utility-scale power demands, operator market concentration, and the operational impact of grassroots community opposition.

---

## 📌 Executive Summary

* **Geographic Monopolies:** The top 5 states account for **62.7%** of all facilities nationwide. Virginia represents **28.4% (460 sites)**, with Loudoun and Prince William counties alone accounting for **17.3%** of the entire national footprint.
* **The Speculative Wave:** Active operating facilities represent only **36.4%** of the national inventory; **55.7%** sits in pre-operational stages (**45.9% Proposed**, **9.8% Under Construction**). Emerging markets show higher speculative shares (Missouri at **60.6%**, Ohio at **56.9%**).
* **The Gigawatt-Scale Inflection:** While only **9 Mega Campuses (>1,000 MW)** are currently operating in this dataset, there are **64 proposed and 29 under construction**—a **10.3x capacity surge** that substantially increases regional grid demands.
* **Operator Landscape & "LLC Cloaking":** Disclosed operators reveal a market where **51.8%** of sites belong to an extensive long tail (over 80% run a single site). However, Big Tech and wholesale REITs control virtually all >100 MW builds. Furthermore, **44.3%** of all facilities in the dataset operate under anonymous LLC shells to obscure early-stage land acquisition.
* **Grassroots Pushback as a Fatal Risk:** Backlash tracks facility scale: Mega Campuses (>1 GW) face a **41.7% opposition rate**, compared to **8.9%** for small edge facilities. Pushback is an acute indicator of attrition: **60.9% of all cancelled or suspended projects** faced documented community opposition.

---

## 📊 Summary Metrics

| Dimension | Key Metric | Value |
| :--- | :--- | :--- |
| **Total Inventory** | Tracked Facilities | **1,621** |
| **Primary Hub** | Virginia Concentration | **28.4%** (460 sites) |
| **Core Epicenter** | Loudoun County, VA | **189 sites** (11.7% of US total) |
| **Pipeline Ratio** | Operating vs. Pipeline | **36.4%** vs. **55.7%** |
| **Project Attrition** | Cancelled / Suspended | **7.9%** (128 sites) |
| **Dominant Disclosed Tier** | Hyperscale (100–999 MW) | **345 sites** (Median: 285 MW) |
| **Emerging Scale** | Mega Campuses (>1 GW) | **115 sites** (Median: 1,250 MW) |
| **Top Disclosed Operator** | Amazon / AWS | **92 facilities** |
| **Market Long Tail** | Single-Site Operators | **338 companies** (81.8% of disclosed operators) |
| **Attrition Pushback Rate** | Stalled Projects Facing Resistance | **60.9%** |

---

## 🔍 Analytical Modules

### 1. Geospatial Footprint & Administrative Hierarchy
* Analyzed national dispersion across state, county, and city levels.
* Built an interactive multi-tier **Sunburst Chart** (`State -> County -> City`) capturing regional dominance across Northern Virginia, Central Texas, and Greater Atlanta.

### 2. Development Pipeline & Lifecycle Dynamics
* Harmonized lifecycle stages into `Operating`, `Under Construction / Permitted`, `Proposed`, and `Suspended / Cancelled`.
* Constructed normalized stacked distribution profiles tracking speculative vs. energized capacity across leading states.

### 3. Sizing & Disclosed Power Demand (MW)
* Resolved capacity categories across `Small`, `Medium`, `Large`, `Hyperscale`, and `Mega campus`.
* Built regex parsers to convert non-standard megawatt ranges (`100-200 MW`, `1,000+ MW`) into numeric features and visualized log-scale capacity distributions.

### 4. Operator Concentration & Corporate Archetypes
* Harmonized operator entities and segmented the industry into **Big Tech Hyperscalers**, **Wholesale & Colocation REITs**, and **Regional/Independent Developers**.
* Evaluated corporate cloaking practices and market entry barriers.

### 5. Community Resistance & Project Mortality
* Analyzed the geographic distribution of 269 community opposition campaigns.
* Quantified resistance probability relative to facility scale (MW) and correlated pushback with project cancellation rates.

---

## 🛠️ Data Pipeline & Hygiene Notes

The primary dataset originates from watchdog monitoring by **FracTracker Alliance** (incorporating data from the Piedmont Environmental Council and Science for Georgia):
* **Geospatial Completeness:** Location coordinates (`lat`, `long`), `status`, and `sizerank` feature near-100% completeness.
* **ZIP Code Precision:** Addressed pandas integer-to-float truncation bugs where East Coast ZIPs lost leading zeros by enforcing zero-padded string casting (`.str.zfill(5)`).
* **Sparse Engineering Fields:** Technical columns such as `cooling_source` (>96% null) and `project_cost` (>83% null) were isolated to avoid reporting bias in quantitative aggregations.
* **Plotly State Slicing:** Interactive visualizations were refactored using `plotly.graph_objects` to enforce trace-level custom data isolation.
