# 💡 Healthkart-Dashboard

## 📝 Overview

This project demonstrates how to build a relational SQLite database from influencer campaign data stored in an Excel file, and how to develop an interactive **Power BI Dashboard** to track key performance metrics such as **Total Revenue**, **Total Spend**, and **ROAS (Return on Ad Spend)**. The dashboard helps analyze campaign effectiveness across platforms and products.

---

## 🎯 Objective

* Convert structured Excel sheets into a relational database
* Import data into **Power BI** and define DAX measures
* Generate insights on campaign ROI, top influencers, and payouts

---

## 🏗️ Project Structure

1. **Database Generation**: Uses Python and `pandas` to read Excel sheets and construct an SQLite database.
2. **Power BI Dashboard**: Connects to the database for modeling, DAX calculations, and insights visualization.
3. **Dashboard Insights**: Showcases KPIs and charts like:

   * Total Revenue
   * Total Spend
   * ROAS & Incremental ROAS
   * Top Influencers by Revenue
   * Product Purchase Trends

---

## 🛠️ Database Generation

### 📂 Requirements

To run the Python script, install the following:

```bash
pip install pandas openpyxl
import pandas as pd
import sqlite3

# Load Excel file
xls = pd.ExcelFile('hk_assnmt.xlsx')
df_payout = pd.read_excel(xls, sheet_name='payout')
df_influencer = pd.read_excel(xls, sheet_name='influencer')
df_tracking = pd.read_excel(xls, sheet_name='tracking data')
df_posts = pd.read_excel(xls, sheet_name='posts')

# Create SQLite DB
conn = sqlite3.connect('hk_assignment.db')
cursor = conn.cursor()

# Drop existing tables
for table in ['payout', 'influencer', 'tracking', 'posts']:
    cursor.execute(f"DROP TABLE IF EXISTS {table}")

# Save new tables
df_payout.to_sql('payout', conn, index=False)
df_influencer.to_sql('influencer', conn, index=False)
df_tracking.to_sql('tracking', conn, index=False)
df_posts.to_sql('posts', conn, index=False)

conn.close()
print("✅ SQLite database 'hk_assignment.db' created successfully.")
📈 Power BI Dashboard Steps
1. Import Data
- Open Power BI Desktop
- Go to Home > Get Data > SQLite
- Select hk_assignment.db and import the four tables
2. Create Relationships
- In Model View, link tables by influencer_id:
- Influencer ↔ Posts
- Influencer ↔ Tracking
- Influencer ↔ Payouts
3. Add Measures
Total Revenue = SUM(Tracking[revenue])

Total Spend = SUMX(Payout, Payout[rate] * Payout[orders])

ROAS = DIVIDE([Total Revenue], [Total Spend])


📊 Visualizations
- Bar Charts: Top Influencers by Revenue, Most Purchased Products
- Line Chart: ROAS over Time
- Pie Charts: Platform Performance, Gender Distribution
- KPIs: Total Revenue, Total Spend, ROAS

💡 Insights
- Top Influencers: Revenue comparison (e.g. Julia Bennett, Christina Camacho)
- ROAS Trends: Track ROI efficiency month-by-month
- Brand Performance: Gritzo emerges as top-selling product
- Platform ROI: Breakdown of engagement across Instagram, YouTube, Twitter
- Diversity Check: Gender and category distribution of influencers

🔗 Resources
- Dashboard PDF: 
- Database Script: Included above
- Excel Source File: hk_assnmt.xlsx — manually added to the repository
- Power BI File: campaign_dashboard.pbix

👨‍💻 Created by Vishesh
This project applies structured guidance and iterative refinement across data modeling, visual storytelling, and campaign analytics.

⚙️ Tools & Technologies
- Python (pandas, openpyxl, sqlite3)
- Power BI Desktop
- Excel

🙌 Contributions Welcome
Feedback, ideas, and enhancements are always appreciated. Let’s decode influencer performance and build smarter dashboards together 🔍📈

---

