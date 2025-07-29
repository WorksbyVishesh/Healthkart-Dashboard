# **Healthkart-Dashboard**

## **Overview**

This project demonstrates how to simulate data for influencer marketing campaigns and build an interactive **Power BI Dashboard** to track key performance metrics such as **Total Revenue**, **Total Spend**, **Return on Ad Spend (ROAS)**, and more. The dashboard provides insights into the effectiveness of influencer campaigns across various platforms and products.

## **Objective**

The goal of this project is to:

* **Generate synthetic data** for influencer campaigns, posts, tracking data, and payouts.
* **Analyze the data** using Power BI to track **ROI (ROAS)**, **performance over time**, and **influencer effectiveness**.
* **Generate insights** such as top influencers, most purchased products, and influencer payouts.

---

## **Project Structure**

1. **Data Generation**: The data is simulated using **Python**. Synthetic data includes influencers, their posts, campaign performance data, and payout details.
2. **Power BI Dashboard**: The data is then imported into **Power BI**, where relationships are set up, and key performance metrics are calculated using DAX. Interactive visualizations show trends, insights, and comparisons.
3. **Dashboard Insights**: The final dashboard presents metrics such as:

   * Total Revenue
   * Total Spend
   * Incremental ROAS
   * Top Influencers by Revenue
   * Most Purchased Products

---

## **Data Generation**

### **Data Generation with Python**

The dataset is generated using Python and sqlite3, with the following key attributes:

* **Influencers**: Simulated with attributes like ID, name, category, gender, follower count, and platform.
* **Posts**: Each influencer has posts with details like platform, date, URL, reach, likes, and comments.
* **Tracking Data**: Contains data such as source, campaign, product, orders, and revenue for each influencer's post.
* **Payouts**: Simulated payouts based on posts or orders, showing the total payout per influencer.

### **Dependencies**

To run the Python data generation script, install the required dependencies:

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

## **Power BI Dashboard**

### **1. Import Data into Power BI**

* Open **Power BI Desktop**.
* Go to **Home** > **Get Data** > **Text/CSV**.
* Import the following CSV files:

  * `influencers.csv`
  * `posts.csv`
  * `tracking_data.csv`
  * `payouts.csv`
* Click **Load** to load the data into Power BI.

### **2. Create Relationships**

* Go to the **Model** view and create relationships between the tables based on `influencer_id`:

  * **Influencers** <-> **Posts**
  * **Influencers** <-> **Tracking Data**
  * **Influencers** <-> **Payouts**

### **3. Create Calculated Measures**

* **Total Revenue**:

  ```DAX
  Total Revenue = SUM(TrackingData[revenue])
  ```
* **Total Spend**:

  ```DAX
  Total Spend = SUMX(Payouts, Payouts[rate] * Payouts[orders])
  ```
* **ROAS**:

  ```DAX
  ROAS = DIVIDE([Total Revenue], [Total Spend])
  ```

### **4. Create Visualizations**

* **Bar Charts** for **Top Influencers by Revenue** and **Most Purchased Products by Users**.
* **Line Chart** for **ROAS over Time**.
* **Pie Charts** for **Performance by Platform** and **Influencers by Gender**.
* **KPIs** to display **Total Revenue**, **Total Spend**, and **Incremental ROAS**.

---

## **Insights from the Dashboard**

### **Top Influencers by Revenue**

This visualization ranks influencers based on the total revenue they generated. Key insights include identifying the top-performing influencers, like **LIFTBOSS** and **FITGURU**, who drive the most revenue.

### **ROAS Over Time**

This line chart helps track the efficiency of campaigns by comparing **ROAS** over several months. It shows trends in campaign effectiveness, helping identify opportunities to improve return on ad spend.

### **Most Purchased Products by Users**

By analyzing the number of orders for each product, this chart reveals which products are driving the most sales. **Gritzo** emerged as the top-performing product.

### **Influencer Payout Analysis**

This table provides a detailed analysis of payouts per influencer based on posts or orders. **Fitguru** and **Nutrinova** stand out in terms of payout, with a higher number of orders or posts.

### **Platform Performance**

This pie chart breaks down campaign performance across platforms (e.g., **YouTube** vs **Twitter**), helping marketers decide where to allocate future resources.

### **Gender Distribution of Influencers**

This chart shows the gender distribution of influencers. The analysis can help ensure diversity in future campaigns and reveal any skewed trends toward male or female influencers.

---

## **Links to Project Resources**

* **Power BI Dashboard**: https://github.com/WorksbyVishesh/Healthkart-_Dashboard-_Assignment/edit/main/README.md
* **CSV Files**:
  [Influencer]https://github.com/WorksbyVishesh/Healthkart-_Dashboard-_Assignment/edit/main/README.md
  [Payout]https://github.com/WorksbyVishesh/Healthkart-_Dashboard-_Assignment/edit/main/README.md
  [Posts]https://github.com/WorksbyVishesh/Healthkart-_Dashboard-_Assignment/edit/main/README.md
  [Tracking_data]https://github.com/WorksbyVishesh/Healthkart-_Dashboard-_Assignment/edit/main/README.md
  

* **Data Model**: [Data Model Explanation]https://github.com/WorksbyVishesh/Healthkart-_Dashboard-_Assignment/edit/main/README.md

---

### **Conclusion**

This project showcases how to simulate influencer campaign data and build a Power BI dashboard for actionable insights on campaign performance, influencer effectiveness, and product sales. The dashboard provides valuable tools to optimize future influencer marketing strategies.

---
