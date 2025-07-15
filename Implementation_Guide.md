# Zepto Sales Analysis Power BI Implementation Guide

## Prerequisites
- Power BI Desktop installed on your system
- Basic understanding of Power BI interface
- Sample data file (zepto_sales_data.csv) ready for import

## Step 1: Data Import and Setup

### 1.1 Load Data into Power BI
1. Open Power BI Desktop
2. Click "Get Data" > "Text/CSV"
3. Browse to `zepto_sales_data.csv` and select it
4. In the preview window, verify data looks correct
5. Click "Load" to import the data

### 1.2 Data Type Configuration
1. Go to "Data" view (table icon on the left)
2. Select the `zepto_sales_data` table
3. Set appropriate data types:
   - Date: Date
   - Order_ID: Text
   - Product_Category: Text
   - Product_Name: Text
   - Quantity: Whole Number
   - Unit_Price: Decimal Number
   - Total_Sales: Decimal Number
   - Customer_ID: Text
   - Outlet_Tier: Text
   - City: Text
   - Customer_Rating: Decimal Number
   - Delivery_Time_Minutes: Whole Number
   - Payment_Method: Text

## Step 2: Create Calculated Columns

### 2.1 Add Time-Based Columns
1. In Data view, right-click on the table
2. Select "New Column"
3. Add the following calculated columns:

```DAX
Month-Year = FORMAT('zepto_sales_data'[Date], "MMM YYYY")
```

```DAX
Day of Week = FORMAT('zepto_sales_data'[Date], "dddd")
```

```DAX
Sales Performance = 
SWITCH(
    TRUE(),
    'zepto_sales_data'[Total_Sales] >= 200, "High",
    'zepto_sales_data'[Total_Sales] >= 100, "Medium",
    "Low"
)
```

```DAX
Delivery Performance = 
SWITCH(
    TRUE(),
    'zepto_sales_data'[Delivery_Time_Minutes] <= 10, "Excellent",
    'zepto_sales_data'[Delivery_Time_Minutes] <= 15, "Good",
    'zepto_sales_data'[Delivery_Time_Minutes] <= 20, "Average",
    "Poor"
)
```

```DAX
Customer Satisfaction = 
SWITCH(
    TRUE(),
    'zepto_sales_data'[Customer_Rating] >= 4.5, "Excellent",
    'zepto_sales_data'[Customer_Rating] >= 4.0, "Good",
    'zepto_sales_data'[Customer_Rating] >= 3.5, "Average",
    "Poor"
)
```

## Step 3: Create Measures

### 3.1 Basic Measures
1. Go to "Report" view
2. Right-click on the table in the Fields pane
3. Select "New Measure"
4. Create the following measures:

```DAX
Total Sales = SUM('zepto_sales_data'[Total_Sales])
```

```DAX
Total Orders = COUNTROWS('zepto_sales_data')
```

```DAX
Average Order Value = DIVIDE([Total Sales], [Total Orders], 0)
```

```DAX
Average Rating = AVERAGE('zepto_sales_data'[Customer_Rating])
```

```DAX
Average Delivery Time = AVERAGE('zepto_sales_data'[Delivery_Time_Minutes])
```

### 3.2 Advanced Measures
```DAX
Sales Growth MoM = 
VAR CurrentMonthSales = [Total Sales]
VAR PreviousMonthSales = CALCULATE(
    [Total Sales],
    DATEADD('zepto_sales_data'[Date], -1, MONTH)
)
RETURN
DIVIDE(CurrentMonthSales - PreviousMonthSales, PreviousMonthSales, 0)
```

```DAX
High Rating Orders = 
CALCULATE(
    [Total Orders],
    'zepto_sales_data'[Customer_Rating] >= 4.5
)
```

```DAX
Fast Delivery Orders = 
CALCULATE(
    [Total Orders],
    'zepto_sales_data'[Delivery_Time_Minutes] <= 12
)
```

```DAX
UPI Payment Share = 
DIVIDE(
    CALCULATE([Total Orders], 'zepto_sales_data'[Payment_Method] = "UPI"),
    [Total Orders],
    0
)
```

## Step 4: Create Executive Summary Page

### 4.1 Page Setup
1. Add a new page and rename it "Executive Summary"
2. Set page size to 16:9 (Page Settings > Page Size)
3. Choose appropriate background color

### 4.2 Add KPI Cards
1. **Total Sales Card**
   - Visual: Card
   - Fields: Total Sales measure
   - Format: Currency, Indian Rupees
   - Add trend indicator using conditional formatting

2. **Total Orders Card**
   - Visual: Card
   - Fields: Total Orders measure
   - Format: Whole number

3. **Average Order Value Card**
   - Visual: Card
   - Fields: Average Order Value measure
   - Format: Currency

4. **Average Rating Card**
   - Visual: Card
   - Fields: Average Rating measure
   - Format: 1 decimal place

5. **Average Delivery Time Card**
   - Visual: Card
   - Fields: Average Delivery Time measure
   - Format: Whole number with "min" suffix

### 4.3 Add Main Charts
1. **Sales Trend Line Chart**
   - Visual: Line chart
   - X-axis: Month-Year
   - Y-axis: Total Sales
   - Enable analytics trend line

2. **Category Sales Donut Chart**
   - Visual: Donut chart
   - Legend: Product_Category
   - Values: Total Sales
   - Enable data labels with percentages

3. **City Performance Bar Chart**
   - Visual: Horizontal bar chart
   - Y-axis: City
   - X-axis: Total Sales
   - Color: Outlet_Tier

4. **Customer Satisfaction Chart**
   - Visual: Stacked column chart
   - X-axis: Customer Satisfaction
   - Y-axis: Total Orders
   - Color: Customer Satisfaction

## Step 5: Create Sales Performance Deep Dive Page

### 5.1 Page Setup
1. Add new page: "Sales Performance"
2. Set 16:9 layout

### 5.2 Add Slicers
1. **Date Range Slicer**
   - Visual: Date range slicer
   - Field: Date
   - Format: Calendar style

2. **Product Category Slicer**
   - Visual: Dropdown slicer
   - Field: Product_Category
   - Enable multi-select

3. **City Slicer**
   - Visual: List slicer
   - Field: City
   - Enable multi-select

4. **Outlet Tier Slicer**
   - Visual: Button slicer
   - Field: Outlet_Tier

### 5.3 Add Analysis Charts
1. **Monthly Sales Comparison**
   - Visual: Clustered column chart
   - X-axis: Month-Year
   - Y-axis: Total Sales
   - Add previous period comparison

2. **Top Products Table**
   - Visual: Table
   - Columns: Product_Name, Product_Category, Total Sales, Quantity
   - Sort by Total Sales descending
   - Add conditional formatting

3. **Sales Performance Matrix**
   - Visual: Matrix
   - Rows: Product_Category
   - Columns: City
   - Values: Total Sales
   - Add heat map formatting

## Step 6: Create Operational Analytics Page

### 6.1 Add Operational KPIs
1. **Fast Delivery Orders Gauge**
   - Visual: Gauge
   - Value: Fast Delivery Orders percentage
   - Target: 80%

2. **High Rating Orders Gauge**
   - Visual: Gauge
   - Value: High Rating Orders percentage
   - Target: 70%

3. **UPI Payment Share Gauge**
   - Visual: Gauge
   - Value: UPI Payment Share
   - Target: 50%

### 6.2 Add Performance Charts
1. **Delivery Time Histogram**
   - Visual: Histogram
   - X-axis: Delivery_Time_Minutes
   - Y-axis: Count
   - Color: Delivery Performance

2. **Rating vs Delivery Time Scatter Plot**
   - Visual: Scatter plot
   - X-axis: Delivery_Time_Minutes
   - Y-axis: Customer_Rating
   - Size: Total_Sales
   - Color: Outlet_Tier

## Step 7: Create Customer Insights Page

### 7.1 Customer Analysis Charts
1. **Customer Rating Distribution**
   - Visual: Histogram
   - X-axis: Customer_Rating
   - Y-axis: Count
   - Color: Customer Satisfaction

2. **City Performance Map**
   - Visual: Map
   - Location: City
   - Size: Total Sales
   - Color: Average Rating

## Step 8: Add Interactive Features

### 8.1 Configure Cross-Filtering
1. Select each visual and configure interactions
2. Enable/disable cross-filtering as needed
3. Set up drill-through functionality

### 8.2 Add Bookmarks
1. Create bookmarks for key insights
2. Add navigation buttons
3. Set up bookmark actions

## Step 9: Apply Formatting and Styling

### 9.1 Color Scheme
1. Go to Format pane for each visual
2. Apply consistent color scheme:
   - Primary: Purple (#6B46C1)
   - Secondary: Green (#10B981)
   - Accent: Orange (#F59E0B)

### 9.2 Typography
1. Set consistent fonts across all visuals
2. Use Segoe UI for headers and labels
3. Apply appropriate font sizes

### 9.3 Conditional Formatting
1. Apply color rules for performance metrics
2. Use data bars for numerical comparisons
3. Add icons for trend indicators

## Step 10: Testing and Optimization

### 10.1 Test Interactivity
1. Test all slicers and filters
2. Verify cross-filtering works correctly
3. Check drill-through functionality

### 10.2 Performance Optimization
1. Review query performance
2. Optimize DAX measures
3. Check data refresh times

### 10.3 Mobile Layout
1. Create mobile-optimized layouts
2. Test on different screen sizes
3. Adjust visual placement for mobile

## Step 11: Publishing and Sharing

### 11.1 Save and Publish
1. Save the .pbix file
2. Publish to Power BI Service
3. Configure refresh schedule

### 11.2 Set Up Sharing
1. Create workspace for collaboration
2. Set up row-level security if needed
3. Configure sharing permissions

### 11.3 Create Subscriptions
1. Set up email subscriptions
2. Configure alerts for key metrics
3. Create mobile app access

## Tips for Success

1. **Data Quality**: Ensure your data is clean and consistent
2. **Performance**: Use measures instead of calculated columns where possible
3. **User Experience**: Keep navigation intuitive and responsive
4. **Storytelling**: Structure your dashboard to tell a compelling story
5. **Maintenance**: Set up regular data refresh and validation processes

## Troubleshooting Common Issues

1. **Slow Performance**: Check DAX formulas and reduce complex calculations
2. **Filter Issues**: Verify field relationships and filter contexts
3. **Visual Errors**: Check data types and measure definitions
4. **Refresh Failures**: Validate data source connections and permissions

This comprehensive implementation guide will help you create a professional, interactive Zepto sales analysis dashboard that provides actionable insights for data-driven decision making.
