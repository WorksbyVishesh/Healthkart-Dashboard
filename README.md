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

1. **Data Generation**: The data is simulated using **Python** and the **Faker** library. Synthetic data includes influencers, their posts, campaign performance data, and payout details.
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

The dataset is generated using Python, with the following key attributes:

* **Influencers**: Simulated with attributes like ID, name, category, gender, follower count, and platform.
* **Posts**: Each influencer has posts with details like platform, date, URL, reach, likes, and comments.
* **Tracking Data**: Contains data such as source, campaign, product, orders, and revenue for each influencer's post.
* **Payouts**: Simulated payouts based on posts or orders, showing the total payout per influencer.

### **Dependencies**

To run the Python data generation script, install the required dependencies:

import pandas as pd
import numpy as np
import random

# Seed for reproducibility
np.random.seed(42)

# --- 1. Influencer Table ---
influencer_data = []
names = ['FitGuru', 'YogaQueen', 'LiftBoss', 'NutriNova', 'FlexKing']
categories = ['Fitness', 'Wellness', 'Bodybuilding', 'Nutrition', 'Fitness']
genders = ['Male', 'Female', 'Male', 'Female', 'Male']
followers = [50000, 75000, 62000, 42000, 55000]
platforms = ['Instagram', 'YouTube', 'Instagram', 'Twitter', 'Instagram']

for i in range(1, 6):
    influencer_data.append([i, names[i-1], categories[i-1], genders[i-1], followers[i-1], platforms[i-1]])

df_influencer = pd.DataFrame(influencer_data, columns=[
    'ID', 'Name', 'Category', 'Gender', 'Follower_Count', 'Platform'
])

# --- 2. Payout Table ---
payout_data = [
    [1, 'Order', 100, 2, 200],
    [2, 'Post', 300, 1, 300],
    [3, 'Order', 120, 3, 360],
    [4, 'Order', 90, 2, 180],
    [5, 'Post', 250, 1, 250]
]

df_payout = pd.DataFrame(payout_data, columns=[
    'Influencer_ID', 'Basis', 'Rate', 'Orders', 'Total_Payout'
])

# --- 3. Tracking Data Table ---
sources = ['Instagram', 'YouTube', 'Instagram', 'Twitter', 'Instagram']
campaigns = ['JulyGains', 'FlexFlow', 'MuscleRush', 'DailyVital', 'RecoveryZone']
brands = ['Gritzo', 'Muscleblaze', 'Hkvital', 'Gritzo', 'Hkvital']
dates = pd.date_range('2025-07-02', periods=5, freq='D')
tracking_data = []

for i in range(5):
    tracking_data.append([
        sources[i], campaigns[i], i+1, f"U00{i+1}",
        dates[i], random.randint(1, 3),
        round(random.uniform(399, 1199), 2), brands[i]
    ])

df_tracking = pd.DataFrame(tracking_data, columns=[
    'Source', 'Campaign', 'Influencer_ID', 'User_ID', 'Date',
    'Orders', 'Revenue', 'Brands'
])

# --- 4. Posts Table ---
urls = [
    'http://insta.com/p1', 'http://youtube.com/p2', 'http://insta.com/p3',
    'http://twitter.com/p4', 'http://insta.com/p5'
]
captions = [
    'Boost your gains!', 'Stay centered, stay strong.', 'Flex your hustle!',
    'Your health, your terms.', 'No pain, no protein!'
]
post_data = []

for i in range(5):
    post_data.append([
        i+1, platforms[i], dates[i] - pd.Timedelta(days=1), urls[i], captions[i],
        random.randint(9000, 15000), random.randint(600, 1200), random.randint(40, 90)
    ])

df_posts = pd.DataFrame(post_data, columns=[
    'Influencer_ID', 'Platform', 'Date', 'URL', 'Caption',
    'Reach', 'Likes', 'Comments'
])

# --- Save to CSV ---
df_influencer.to_csv('influencer.csv', index=False)
df_payout.to_csv('payout.csv', index=False)
df_tracking.to_csv('tracking_data.csv', index=False)
df_posts.to_csv('posts.csv', index=False)


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

This visualization ranks influencers based on the total revenue they generated. Key insights include identifying the top-performing influencers, like **Christina Camacho** and **Julia Bennett**, who drive the most revenue.

### **ROAS Over Time**

This line chart helps track the efficiency of campaigns by comparing **ROAS** over several months. It shows trends in campaign effectiveness, helping identify opportunities to improve return on ad spend.

### **Most Purchased Products by Users**

By analyzing the number of orders for each product, this chart reveals which products are driving the most sales. **Gritzo** emerged as the top-performing product.

### **Influencer Payout Analysis**

This table provides a detailed analysis of payouts per influencer based on posts or orders. **Brian Johnson** and **Chelsea Murray** stand out in terms of payout, with a higher number of orders or posts.

### **Platform Performance**

This pie chart breaks down campaign performance across platforms (e.g., **YouTube** vs **Twitter**), helping marketers decide where to allocate future resources.

### **Gender Distribution of Influencers**

This chart shows the gender distribution of influencers. The analysis can help ensure diversity in future campaigns and reveal any skewed trends toward male or female influencers.

---

## **Links to Project Resources**

* **Power BI Dashboard**: 
* **CSV Files**:

  * [Influencers Data](https://github.com/Jaideepgupta/Healthkart-Dashboard/blob/main/influencers.csv)
  * [Posts Data](https://github.com/Jaideepgupta/Healthkart-Dashboard/blob/main/posts.csv)
  * [Tracking Data](https://github.com/Jaideepgupta/Healthkart-Dashboard/blob/main/tracking_data.csv)
  * [Payouts Data](https://github.com/Jaideepgupta/Healthkart-Dashboard/blob/main/payouts.csv)
* **Data Model**: [Data Model Explanation](https://github.com/Jaideepgupta/Healthkart-Dashboard/blob/main/Data%20Model.png)

---

### **Conclusion**

This project showcases how to simulate influencer campaign data and build a Power BI dashboard for actionable insights on campaign performance, influencer effectiveness, and product sales. The dashboard provides valuable tools to optimize future influencer marketing strategies.

---
