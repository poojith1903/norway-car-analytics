# Norway Car Sales Analytics Dashboard

[![Power BI](https://img.shields.io/badge/Power%20BI-Dashboard-F2C811.svg)](https://powerbi.microsoft.com)
[![Excel](https://img.shields.io/badge/Excel-Data%20Source-217346.svg)](https://microsoft.com/excel)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)

## Executive Summary

This project delivers a comprehensive Power BI dashboard analyzing car sales performance in the Norwegian automotive market. The solution provides actionable insights into brand performance, revenue generation, market share distribution, and sales trends across seven major automotive manufacturers: Hyundai, BMW, Audi, Ford, Toyota, Skoda, and Volkswagen.

## Project Architecture

```
norway-car-analytics/
├── data/
│   ├── source/
│   │   ├── cars_dataset.xlsx
│   │   │   ├── cars_dataset (sheet)
│   │   │   └── Brands_Master Data (sheet)
│   │   └── Norway_car_sales_by_make.csv
│   └── processed/
│       └── cars-project.pbix
├── documentation/
│   ├── project_requirements.md
│   ├── data_dictionary.md
│   └── dashboard_guide.md
├── assets/
│   ├── brand_logos/
│   └── screenshots/
└── README.md
```

## Dataset Specifications

### Primary Data Sources

#### 1. cars_dataset.xlsx
**Multi-sheet Excel workbook containing vehicle specifications and brand information**

**Sheet A: cars_dataset**
| Field | Type | Description | Sample Values |
|-------|------|-------------|---------------|
| `model` | String | Vehicle model name | "Golf", "Corolla", "X5" |
| `year` | Integer | Manufacturing year | 2018, 2019, 2020, 2021 |
| `price` | Currency | Vehicle retail price (NOK) | 250000, 450000, 750000 |
| `transmission` | Categorical | Transmission type | "Manual", "Automatic" |
| `mileage` | Integer | Fuel efficiency (km/l) | 15, 18, 22 |
| `fuelType` | Categorical | Primary fuel source | "Petrol", "Diesel", "Electric", "Hybrid" |
| `tax` | Currency | Annual vehicle tax (NOK) | 2500, 5000, 8500 |
| `engineSize` | Float | Engine displacement (L) | 1.6, 2.0, 3.0 |
| `Make` | String | Vehicle manufacturer | "BMW", "Toyota", "Volkswagen" |

**Sheet B: Brands_Master Data**
| Field | Type | Description |
|-------|------|-------------|
| `Make` | String | Vehicle manufacturer name |
| `Logo` | URL | Brand logo image URL |
| `Image` | URL | Brand promotional image URL |

#### 2. Norway_car_sales_by_make.csv
**Time-series sales data by manufacturer**

| Field | Type | Description | Sample Values |
|-------|------|-------------|---------------|
| `Year` | Integer | Sales year | 2018, 2019, 2020, 2021 |
| `Month` | Integer | Sales month | 1, 2, 3...12 |
| `Make` | String | Vehicle manufacturer | "BMW", "Toyota", "Ford" |
| `Quantity` | Integer | Units sold | 150, 280, 420 |
| `Pct` | Float | Market share percentage | 8.5, 12.3, 15.7 |

## Business Intelligence Requirements

### Key Performance Indicators (KPIs)

1. **Total Units Sold by Brand**
   - Aggregate quantity metrics across all manufacturers
   - Brand-specific performance comparison

2. **Revenue Generation Analysis**
   - Total revenue by car model/variant
   - Revenue contribution by manufacturer

3. **Product Portfolio Diversity**
   - Number of available variants per brand
   - Model availability assessment

4. **Market Valuation Metrics**
   - Brand market value visualization via bar charts
   - Comparative brand positioning

5. **Top Performer Identification**
   - Top 4 revenue-generating models per brand
   - Performance-based model ranking

6. **Market Share Distribution**
   - Percentage market share by manufacturer
   - Competitive landscape analysis

7. **Temporal Sales Trends**
   - Time-series analysis of sales performance
   - Seasonal and annual trend identification

### Target Manufacturer Focus
Analysis restricted to seven premium automotive brands:
- **Hyundai** | **BMW** | **Audi** | **Ford** | **Toyota** | **Skoda** | **Volkswagen**

## Dashboard Implementation Guide

### Power BI Development Workflow

#### Phase 1: Data Ingestion & Preparation
```powershell
# Data Loading Sequence
1. Excel Workbook Import (cars_dataset.xlsx)
   - Select: Brands_Master Data + cars_dataset sheets
   - Transform: Use First Row as Headers
   
2. CSV Import (Norway_car_sales_by_make.csv)
   - Direct import with automatic type detection
   
3. Data Model Application
   - Close & Apply transformations
```

#### Phase 2: Data Model Configuration
```sql
-- Relationship Establishment
cars_dataset[Make] ←→ Brands_Master Data[Make] (One-to-Many)
Brands_Master Data[Make] ←→ Norway_car_sales_by_make[Make] (One-to-Many)

-- Data Type Optimization
Brands_Master Data[Logo] → Image URL
Brands_Master Data[Image] → Image URL
```

#### Phase 3: Visualization Components

**1. Interactive Brand Selector**
- **Type**: Slicer (Tile Style)
- **Source**: Brands_Master Data[Logo]
- **Layout**: Single-row horizontal arrangement

**2. Performance KPI Cards**
```dax
Units Sold = SUM(Norway_car_sales_by_make[Quantity])
Total Revenue = SUM(cars_dataset[price])
Variant Count = DISTINCTCOUNT(cars_dataset[model])
```

**3. Market Value Analysis**
- **Type**: Stacked Column Chart
- **Axes**: X = Make, Y = price
- **Formatting**: Gold color scheme, centered title

**4. Top Performers Analysis**
- **Type**: Clustered Bar Chart
- **Configuration**: Top N filter (N=4), by Sum of price
- **Sorting**: Descending by revenue

**5. Market Share Visualization**
- **Type**: Pie Chart
- **Data**: Legend = Make, Values = Sum of Quantity
- **Filter**: Limited to 7 target manufacturers

**6. Sales Trend Analysis**
- **Type**: Line Chart
- **Temporal Axis**: Year from Norway_car_sales_by_make
- **Metrics**: Sum of Quantity with 5px orange line styling

### Power BI Service Deployment

#### Publication Process
```powershell
# Deployment Steps
1. File → Publish
2. Select Target Workspace (My workspace)
3. Access via app.powerbi.com
4. Authentication: Enterprise credentials
```

## Key Business Insights

### Market Performance Metrics
- **Total Sales Volume**: 1,347K units across target brands
- **Revenue Concentration**: Premium brands drive higher per-unit revenue
- **Product Diversity**: Varied model portfolios across manufacturers
- **Temporal Trends**: Seasonal sales patterns with year-over-year growth

### Competitive Analysis
- **Market Leadership**: Identification of dominant brands by volume and revenue
- **Portfolio Strategy**: Analysis of variant diversity impact on market share
- **Growth Trajectories**: Time-series trend analysis revealing market dynamics

## Technical Specifications

### System Requirements
- **Power BI Desktop**: Version 2.120.0 or later
- **Excel Compatibility**: Microsoft Excel 2016+
- **Memory**: Minimum 8GB RAM for optimal performance
- **Storage**: 500MB available disk space

### File Dependencies
```
cars_dataset.xlsx (Primary data source)
├── cars_dataset sheet (Vehicle specifications)
└── Brands_Master Data sheet (Brand metadata)

Norway_car_sales_by_make.csv (Sales performance data)
└── Time-series sales metrics by manufacturer
```

### Dashboard Features
- **Interactive Filtering**: Dynamic brand selection via logo slicer
- **Real-time Updates**: Automatic recalculation based on filter selections
- **Visual Consistency**: Professional theming with blue/gold color scheme
- **Export Capabilities**: PDF and PowerPoint export functionality

## Quality Assurance & Validation

### Data Integrity Checks
- **Relationship Validation**: Confirmed Many-to-One connections
- **Null Value Handling**: Blank logo entries filtered from visualizations
- **Aggregation Accuracy**: Manual verification of calculated metrics

### Performance Optimization
- **Query Efficiency**: Optimized DAX expressions for faster rendering
- **Visual Load Times**: Minimized dataset size through focused manufacturer selection
- **Memory Management**: Efficient data model design

## Project Deliverables

### Core Outputs
1. **cars-project.pbix** - Complete Power BI dashboard file
2. **Published Dashboard** - Power BI Service deployment
3. **Technical Documentation** - Implementation guide and specifications

### Stakeholder Benefits
- **Executive Leadership**: High-level market performance overview
- **Sales Teams**: Brand-specific performance insights
- **Marketing Department**: Market share and competitive intelligence
- **Product Management**: Variant performance and portfolio optimization

## Future Enhancement Opportunities

### Advanced Analytics Integration
- **Predictive Modeling**: Sales forecasting using historical trends
- **Customer Segmentation**: Demographic analysis integration
- **Profitability Analysis**: Cost data incorporation for margin analysis

### Technical Improvements
- **Automated Refresh**: Scheduled data updates from live sources
- **Mobile Optimization**: Responsive design for tablet/phone access
- **API Integration**: Real-time data feeds from automotive databases

## Support & Maintenance

### Regular Updates
- **Monthly Data Refresh**: Updated sales figures and new model additions
- **Quarterly Review**: Performance metric validation and insight generation
- **Annual Enhancement**: Dashboard redesign based on user feedback

### Contact Information
- **Technical Support**: Create GitHub issue for dashboard-related problems
- **Data Questions**: Verify source data accuracy and completeness
- **Feature Requests**: Submit enhancement proposals via project tracker

---

**Project Status**: Production Ready | **Last Updated**: July 2024 | **Version**: 1.0.0

*This dashboard serves as a strategic tool for Norwegian automotive market analysis, providing stakeholders with comprehensive insights into brand performance, market dynamics, and sales trends across seven major manufacturers.*
