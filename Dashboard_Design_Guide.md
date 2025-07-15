# Zepto Sales Analysis Dashboard Design Guide

## Dashboard Overview
Create a comprehensive sales dashboard with multiple pages to analyze Zepto's grocery delivery performance across different dimensions.

## Page 1: Executive Summary
### Layout: 16:9 Canvas
**Top Section (KPI Cards)**
- Total Sales (₹) - Card visual with trend indicator
- Total Orders - Card visual with MoM growth
- Average Order Value - Card visual with target comparison
- Average Rating - Card visual with satisfaction gauge
- Average Delivery Time - Card visual with benchmark

**Middle Section (Main Charts)**
- **Sales Trend Over Time** - Line chart showing monthly sales progression
  - X-axis: Month-Year
  - Y-axis: Total Sales
  - Add trend line and forecasting
  
- **Sales by Product Category** - Donut chart
  - Values: Total Sales
  - Legend: Product Categories
  - Show data labels with percentages

**Bottom Section (Performance Metrics)**
- **City Performance** - Horizontal bar chart
  - Y-axis: City names
  - X-axis: Total Sales
  - Color by outlet tier
  
- **Customer Satisfaction Distribution** - Stacked column chart
  - X-axis: Customer Satisfaction levels
  - Y-axis: Count of orders
  - Color by satisfaction rating

## Page 2: Sales Performance Deep Dive
### Layout: 16:9 Canvas
**Top Section (Interactive Filters)**
- Date Range Slicer (Calendar type)
- Product Category Slicer (Dropdown)
- City Slicer (Multi-select)
- Outlet Tier Slicer (Button style)

**Main Analysis Section**
- **Monthly Sales Comparison** - Clustered column chart
  - X-axis: Month-Year
  - Y-axis: Total Sales
  - Series: Current vs Previous period
  
- **Top Products by Revenue** - Table visual
  - Columns: Product Name, Category, Total Sales, Quantity, AOV
  - Sort by Total Sales descending
  - Add conditional formatting for sales values

- **Sales Performance Matrix** - Matrix visual
  - Rows: Product Category
  - Columns: City
  - Values: Total Sales
  - Add heat map conditional formatting

**Bottom Section**
- **Payment Method Distribution** - Pie chart
  - Values: Order count
  - Legend: Payment methods
  
- **Revenue Bucket Analysis** - Funnel chart
  - Values: Premium, Standard, Basic revenue buckets
  - Show conversion rates

## Page 3: Operational Analytics
### Layout: 16:9 Canvas
**Top Section (Operational KPIs)**
- Fast Delivery Orders (%) - Gauge visual
- High Rating Orders (%) - Gauge visual
- UPI Payment Share (%) - Gauge visual
- Customer Loyalty Score - Gauge visual

**Middle Section (Delivery Performance)**
- **Delivery Time Analysis** - Histogram
  - X-axis: Delivery time bins
  - Y-axis: Order count
  - Color by delivery performance category
  
- **Rating vs Delivery Time** - Scatter plot
  - X-axis: Delivery Time
  - Y-axis: Customer Rating
  - Size: Order value
  - Color: Outlet tier

**Bottom Section (Trend Analysis)**
- **Weekly Performance Trends** - Line chart
  - X-axis: Week
  - Y-axis: Multiple metrics (Sales, Orders, Rating)
  - Multiple lines for different metrics
  
- **Day of Week Analysis** - Column chart
  - X-axis: Day of week
  - Y-axis: Total sales
  - Color by weekend/weekday

## Page 4: Customer Insights
### Layout: 16:9 Canvas
**Customer Behavior Analysis**
- **Customer Rating Distribution** - Histogram
  - X-axis: Rating ranges
  - Y-axis: Customer count
  - Color by satisfaction levels
  
- **Order Frequency Analysis** - Bar chart
  - X-axis: Order frequency buckets
  - Y-axis: Customer count
  - Show repeat customer percentage
  
- **AOV by Customer Segment** - Box plot
  - X-axis: Customer segments
  - Y-axis: Order value distribution
  - Show outliers and quartiles

**Geographic Performance**
- **City Performance Map** - Map visual
  - Location: City
  - Size: Total Sales
  - Color: Average Rating
  - Add tooltips with key metrics

## Interactive Features Setup

### Slicers Configuration
1. **Date Range Slicer**
   - Type: Between slicer
   - Field: Date
   - Format: Calendar view
   - Default: Last 3 months

2. **Product Category Slicer**
   - Type: Dropdown
   - Field: Product_Category
   - Multi-select: Yes
   - Search enabled: Yes

3. **City Filter**
   - Type: Button style
   - Field: City
   - Multi-select: Yes
   - Show "All" option

4. **Outlet Tier Filter**
   - Type: Radio buttons
   - Field: Outlet_Tier
   - Single select
   - Default: All

### Cross-Filtering Setup
- Enable cross-filtering between related visuals
- Set up drill-through from summary to detailed views
- Configure bookmarks for key insights

## Visual Formatting Guidelines

### Color Scheme
- Primary: Zepto brand colors (Purple/Green theme)
- Secondary: Complementary colors for categories
- Alerts: Red for negative trends, Green for positive

### Typography
- Headers: Segoe UI, Bold, 16pt
- Metrics: Segoe UI, Regular, 14pt
- Labels: Segoe UI, Regular, 10pt

### Conditional Formatting Rules
1. **Sales Performance**
   - Green: Above target (>₹200)
   - Yellow: Meeting target (₹100-₹200)
   - Red: Below target (<₹100)

2. **Customer Rating**
   - Green: Excellent (4.5+)
   - Yellow: Good (4.0-4.4)
   - Red: Poor (<4.0)

3. **Delivery Time**
   - Green: Fast (≤12 min)
   - Yellow: Average (13-18 min)
   - Red: Slow (>18 min)

## Dashboard Navigation
- Add navigation buttons between pages
- Include a home/summary page link on each page
- Add refresh data button and last update timestamp

## Performance Optimization
- Use aggregated measures instead of calculated columns where possible
- Implement proper data types for all fields
- Use DirectQuery for large datasets
- Set up incremental refresh for historical data

## Mobile Responsive Design
- Create mobile-optimized layouts
- Use responsive visuals
- Prioritize key metrics for mobile view
- Test on different screen sizes

## Export and Sharing Options
- Enable PDF export for executive reports
- Set up automated refresh schedules
- Configure row-level security for different user groups
- Add subscription options for key stakeholders
