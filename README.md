# 🏥 Hospital ER Operations & Patient Flow Analysis

### 📄 Executive Summary
This project is an end-to-end operational analysis designed to reduce Emergency Room wait times and improve patient satisfaction. Unlike static reports, this solution features an **automated ETL pipeline** using Python and the Google Sheets API to feed a live Power BI dashboard.

**Key Business Insight:**
The analysis established a critical **"Patience Threshold" of 60 minutes**. Wait times exceeding this limit result in a sharp 20% drop in patient satisfaction. The primary bottleneck was identified as **Night Shift Orthopedics**, where staffing gaps caused delays despite lower patient volume.

---

### 📊 Dashboard Preview

**AI Diagnostic Lab (Decomposition Tree):**
![Decomposition Tree](Screenshots/decomposition_tree.png)
*(Note: Rename your screenshot to match this)*

---

### ❓ Business Problem
The Hospital Administrator needed to understand why "Average Wait Time" was increasing despite stable patient volume. The goals were:
1.  **Identify Bottlenecks:** Which specific shift or department is failing?
2.  **Define SLAs:** What is the maximum acceptable wait time before satisfaction crashes?
3.  **Automate Reporting:** Replace manual CSV exports with a live data feed.

### 🛠️ Tech Stack & Architecture
* **ETL Pipeline (Python):** * Used **Pandas** to clean raw logs, impute missing satisfaction scores with median values, and engineer features (e.g., "Shift" logic based on timestamps).
    * **Automation:** Integrated the **Google Sheets API** to push cleaned data from a cloud notebook (Colab) to a staging layer, enabling 1-click refreshes in Power BI.
* **Power BI:**
    * **AI Visuals:** Utilized the **Decomposition Tree** for Root Cause Analysis and **Key Influencers** to detect drivers of low satisfaction.
    * **Modeling:** Built a Star Schema with a dedicated Date Dimension to enable Day-of-Week analysis.

### 📈 Key Analysis Steps

#### 1. Automated Data Engineering
Instead of manual Excel cleaning, I wrote a reproducible Python script that:
* Standardized column headers.
* Calculated "Age Buckets" (Pediatric vs. Senior).
* Flagged "Peak Hours" based on arrival timestamps.

#### 2. Root Cause Analysis (RCA)
Using the **AI Decomposition Tree**, I drilled down into the "Average Wait Time" metric.
* **Finding:** While "General Practice" has the most patients, **"Orthopedics"** has the longest delays.
* **Root Cause:** The delay is strictly isolated to the **Night Shift (10 PM - 6 AM)**, indicating a specific staffing shortage during handover hours.

#### 3. Operational Rhythm (Heatmap)
* **Visual:** Peak Hour Heatmap.
* **Insight:** Monday Mornings (8 AM - 11 AM) show the highest density of long wait times, suggesting a backlog from the weekend that isn't being cleared fast enough.

---

### 📉 Visual Insights

**The Patience Threshold:**
![Line Chart](Screenshots/patience_threshold.png)
*Shows the correlation between Wait Time and Satisfaction Score, defining the 60-minute SLA.*

**Operations Heatmap:**
![Heatmap](Screenshots/heatmap.png)
*Visualizing the "Red Zone" on Monday mornings.*

---

### 💡 Recommendations
1.  **Staffing:** Deploy one additional Orthopedic specialist during the Night Shift (10 PM - 6 AM) to address the primary bottleneck.
2.  **Process:** Implement a "Fast Track" triage for Monday mornings to clear the weekend backlog before 11 AM.
3.  **Target:** Set the operational KPI for Wait Time to **<60 minutes** to maintain satisfaction scores above 7/10.
