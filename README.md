# SQL_PowerBI_Socialmedia_Marketing_Analysis

📊 **Comprehensive Marketing Campaign Analysis**: This project analyzes the performance of multiple marketing campaigns, focusing on customer engagement, conversion rates, campaign effectiveness, and revenue generation. Using Power BI, advanced DAX, and SQL, I derived critical insights that allow marketers to make data-driven decisions and optimize future campaigns.

🔍 **Explore advanced DAX calculations, data transformation techniques, and high-level SQL queries** to evaluate how different campaigns, marketing channels, and customer segments contribute to the overall marketing strategy.

# Background

The **Marketing Campaign Analysis** was developed to provide an in-depth understanding of the performance of marketing initiatives across various channels (email, social media, direct mail). The focus is on understanding customer engagement, conversion rates, and ROI for each campaign. By analyzing how different customer segments and channels contribute to marketing effectiveness, this project helps optimize marketing spend and improve targeting strategies.

### Key Questions Addressed:
1. **Which campaigns generate the highest conversion rates and ROI?**
2. **How do different customer segments respond to various marketing channels?**
3. **Which channels (email, social, direct mail) are most effective for customer acquisition and retention?**
4. **What is the revenue contribution of each campaign, and how does it change over time?**
5. **How can we optimize marketing spend to focus on high-performing campaigns?**

# Tools and Techniques I Used

For this analysis, I used several advanced tools and techniques:
- **Power BI**: The primary platform for building an interactive, user-friendly marketing dashboard.
- **Advanced DAX (Data Analysis Expressions)**: Utilized to calculate marketing KPIs, customer segmentation, funnel tracking, and campaign performance metrics.
- **SQL**: Employed to clean, aggregate, and transform the marketing dataset.
- **Conditional Formatting**: Applied to key metrics such as conversion rates and ROI to visually highlight the most impactful campaigns.
- **Advanced Power BI Features**: Drillthrough, What-If analysis, dynamic segmentation, and custom tooltips.

# The Analysis

### 1. Campaign Performance by Channel

One of the primary objectives was to assess which marketing channels (e.g., email, social media, direct mail) drive the most conversions and revenue. Using Power BI, I broke down campaign performance into key metrics:
- **Conversion Rate by Channel**: Shows how each channel contributes to customer acquisition and campaign success.
- **Cost per Acquisition (CPA)**: A vital metric for understanding the cost-effectiveness of each campaign.

**Advanced DAX for CPA Calculation**:
```dax
CPA = 
DIVIDE(
    [Total Marketing Spend],
    [Total New Customers]
)
```

This measure calculates the **Cost per Acquisition** by dividing the total marketing spend by the number of new customers acquired via each channel.

### 2. Revenue Attribution by Campaign

Revenue attribution helps to understand which campaigns generated the most revenue and how their effectiveness varies over time. By linking sales data with marketing efforts, I could see:
- **Revenue contribution per campaign**.
- **Return on Investment (ROI)** for each channel and campaign.

**Advanced ROI Calculation**:
```dax
ROI = 
DIVIDE(
    [Total Revenue] - [Total Marketing Spend], 
    [Total Marketing Spend]
)
```

This formula calculates the **Return on Investment** for each marketing campaign, showing the profit generated for each dollar of marketing spend.

### 3. Customer Segmentation Analysis

To optimize targeting, I segmented customers based on their engagement levels, demographics, and purchasing behavior:
- **Customer Lifetime Value (CLV)**: Grouping customers by their total spend and segmenting them into high, medium, and low-value groups.
- **Customer Engagement Score**: A composite score based on email open rates, social media interactions, and purchase frequency, ranking customers by their engagement with the brand.

**DAX for Customer Segmentation**:
```dax
Customer Segment = 
SWITCH(
    TRUE(),
    [Customer Lifetime Value] > 5000, "High-Value Customer",
    [Customer Lifetime Value] > 1000, "Mid-Value Customer",
    "Low-Value Customer"
)
```

This advanced DAX formula segments customers based on their **lifetime value**, enabling targeted marketing strategies for different customer tiers.

### 4. Conversion Funnel Tracking

To measure how effectively the campaigns move potential customers through each stage of the funnel, I built a **conversion funnel analysis**:
- **Impressions → Clicks → Leads → Conversions**: A funnel chart that visualizes the conversion rates at each stage.
- **Drop-off Points**: Identifying where the most significant drop-offs occur, allowing for optimization of those specific stages.

**Advanced DAX for Funnel Conversion Rates**:
```dax
Conversion Rate = 
DIVIDE([Total Conversions], [Total Leads])
```

This DAX measure calculates the percentage of leads that convert into customers, helping identify **bottlenecks** in the funnel.

### 5. Time Intelligence for Campaign Performance

Time-based analysis was performed to track campaign performance trends over time. I used **time intelligence** DAX functions to display:
- **Monthly Revenue from Campaigns**: Tracking how each campaign contributes to revenue month-over-month.
- **Year-over-Year Performance**: Comparing campaigns’ performance across different years to identify long-term trends.

**DAX for Month-over-Month Revenue Growth**:
```dax
MoM Revenue Growth = 
VAR CurrentMonth = MAX('Date'[Month])
VAR PreviousMonth = CurrentMonth - 1
RETURN 
DIVIDE(
    [Total Revenue], 
    CALCULATE([Total Revenue], 'Date'[Month] = PreviousMonth)
) - 1
```

This DAX measure tracks **month-over-month revenue growth**, allowing the marketing team to adjust strategies based on short-term performance fluctuations.

### 6. What-If Analysis for Optimizing Marketing Spend

**What-If analysis** was used to simulate how changes in marketing budget allocation would affect key metrics like revenue and customer acquisition. This allowed for scenario planning and optimization of the marketing budget across different channels.

**Advanced What-If Parameter**:
```Power BI
Modeling -> New Parameter -> What-If Parameter -> Define ranges for Marketing Spend.
```

This tool allows for dynamic simulations and gives insights into the impact of different spending strategies on overall campaign performance.

# Advanced SQL Query for Marketing Analysis

Here is an additional advanced SQL query used in the analysis, focusing on calculating the **engagement metrics** across campaigns and channels, while ensuring data quality and consistency:

```sql
WITH CleanedData AS (
    SELECT 
        ProductID,
        Channel,
        EngagementType,
        COUNT(DISTINCT EngagementID) AS TotalEngagements,
        SUM(CASE WHEN EngagementType = 'Click' THEN 1 ELSE 0 END) AS TotalClicks,
        SUM(CASE WHEN EngagementType = 'View' THEN 1 ELSE 0 END) AS TotalViews,
        SUM(CASE WHEN EngagementType = 'Like' THEN 1 ELSE 0 END) AS TotalLikes,
        FORMAT(EngagementDate, 'MMM') AS MonthName
    FROM 
        dbo.fact_engagement_data
    WHERE 
        EngagementDate BETWEEN '2023-01-01' AND '2023-12-31'
    GROUP BY 
        ProductID, Channel, FORMAT(EngagementDate, 'MMM')
)

SELECT 
    ProductID, 
    Channel,
    TotalEngagements,
    TotalClicks,
    TotalViews,
    TotalLikes,
    MonthName
FROM 
    CleanedData
ORDER BY 
    TotalViews DESC;
```

This query aggregates engagement metrics across various marketing channels and products, offering insights into customer engagement and interaction.

# Conditional Formatting

Conditional formatting was applied to highlight key metrics such as **Conversion Rates** and **Customer Lifetime Value**:
- **Conversion Rate**: Campaigns with conversion rates above 10% were highlighted in **green**, while those below 5% were marked in **red**.
- **ROI**: Campaigns with an ROI greater than 200% were marked in **blue** for high performance, while those under 100% were marked in **orange**.

```Power BI
In the visual, select Format -> Conditional Formatting -> Based on field value.
```

# Key Insights

1. **Channel Performance**: This analysis revealed that certain channels (social media, email) consistently outperform others (e.g., direct mail) in terms of conversion rates and ROI.
2. **Customer Segmentation**: High-value customers (based on CLV) are best engaged through targeted campaigns, emphasizing the need for personalized strategies.
3. **Revenue and Conversion Optimization**: With time intelligence and funnel analysis, campaigns can be adjusted based on real-time performance trends, improving the overall return on marketing spend.
4. **What-If Scenarios**: The What-If analysis allowed the team to simulate various marketing strategies, offering valuable insights for optimizing the marketing budget.

# What I Learned

🧩 **Advanced SQL and DAX for Marketing Insights**: I developed proficiency in using SQL and DAX to extract deep insights into campaign performance, customer engagement, and marketing spend optimization
