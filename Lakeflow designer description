# E-Commerce Order Analytics Pipeline
## Built with Databricks Lakeflow Designer

## 📊 Project Overview

A production-ready data pipeline that processes e-commerce order data from multiple sources, performs complex transformations using joins and aggregations, and produces city-level analytics insights. Built entirely using **Databricks Lakeflow Designer's** visual no-code interface.

## 🏗️ Architecture

```
orders (UC Table)          ┐
                           ├──> order_and_items (Full Join)
order_items (UC Table)     ┘                │
                                            │
customers (GitHub CSV) ─────────────────> customer_join (Left Join)
                                            │
shipments (GitHub CSV) ─────────────────> ship_order_cus_join (Left Join)
                                            │
                                         order_by_city (Aggregate)
                                            │
                                         sorted (Sort DESC)
                                            │
                                    aggregated_orders (UC Table)
```

## ✨ Features

- **Multi-Source Data Integration**: Combines data from Unity Catalog tables and external CSV files
- **Complex Join Operations**: Implements full, left, and inner joins across 4 data sources
- **City-Level Analytics**: Aggregates order metrics by geographic location
- **Scalable Architecture**: Built on Apache Spark for distributed processing
- **Automated Data Loading**: Python operators fetch external CSV data from GitHub
- **Delta Lake Output**: Results stored in Unity Catalog for governance and performance

## 📋 Pipeline Components

### Data Sources

1. **Orders Table** (`learning_catalog.raw.orders`)
   - Core order information
   - Source: Unity Catalog managed table

2. **Order Items Table** (`learning_catalog.raw.order_items`)
   - Line-item details for each order
   - Source: Unity Catalog managed table

3. **Customers Data** (CSV)
   - Customer demographic and location data
   - Source: GitHub raw file URL
   - Loading: Python operator with requests + pandas

4. **Shipments Data** (CSV)
   - Shipping and delivery information
   - Source: GitHub raw file URL
   - Loading: Python operator with requests + pandas

### Transformations

1. **order_and_items**: Full join between order_items and orders on `order_id`
2. **customer_join**: Left join to enrich with customer data on `customer_id`
3. **ship_order_cus_join**: Left join to add shipment information on `order_id`
4. **order_by_city**: Aggregates data by city with:
   - `total_order`: Count of orders per city
   - `price_sum`: Total revenue (rounded to 2 decimals)
5. **sorted**: Orders results by total orders (descending)

### Output

- **Table**: `learning_catalog.raw.aggregated_orders`
- **Write Mode**: Overwrite
- **Format**: Delta Lake

## 🛠️ Prerequisites

- **Databricks Workspace** (Community or paid tier)
- **Unity Catalog** enabled
- **Catalog/Schema**: `learning_catalog.raw` (or modify to your catalog)
- **Cluster**: DBR 13.0+ recommended

## 🚀 Setup Instructions

### 1. Clone the Workflow

1. Open Databricks Lakeflow Designer
2. Create a new workflow
3. Import the workflow YAML file from this repository

### 2. Configure Data Sources

**Option A: Use Your Own Tables**
- Replace `learning_catalog.raw.orders` and `learning_catalog.raw.order_items` with your table paths
- Update the catalog and schema in the output operator

**Option B: Create Sample Tables**
```sql
-- Create catalog and schema
CREATE CATALOG IF NOT EXISTS learning_catalog;
CREATE SCHEMA IF NOT EXISTS learning_catalog.raw;

-- Load sample orders and order_items data
-- (Add your CREATE TABLE statements here)
```

### 3. External CSV Sources

The pipeline loads CSV files from GitHub. Current URLs:
- Customers: `https://raw.githubusercontent.com/anshlambagit/Databricks_Lakeflow_Designer/refs/heads/main/customers.csv`
- Shipments: `https://raw.githubusercontent.com/anshlambagit/Databricks_Lakeflow_Designer/refs/heads/main/shipments.csv`

**To use your own CSV files:**
1. Update the `url` variable in the Python operators
2. Ensure CSV format matches expected schema

## 📈 Usage

1. **Open the workflow** in Lakeflow Designer
2. **Run All**: Click the play button to execute the entire pipeline
3. **View Results**: Check the output table `learning_catalog.raw.aggregated_orders`

```sql
SELECT * FROM learning_catalog.raw.aggregated_orders
ORDER BY total_order DESC
LIMIT 10;
```

## 📊 Output Schema

| Column       | Type   | Description                    |
|--------------|--------|--------------------------------|
| city         | STRING | City name                      |
| total_order  | LONG   | Count of orders in that city   |
| price_sum    | DECIMAL| Total revenue (rounded to 2dp) |

## 🔍 Key Insights Generated

- **Top Performing Cities**: Identify which cities generate the most orders
- **Revenue by Location**: Track total sales per geographic area
- **Order Volume Analysis**: Understand customer distribution across regions

## 💡 Technical Highlights

- **No-Code Development**: Built entirely with visual operators
- **Distributed Processing**: Leverages Spark for scalability
- **Data Governance**: Unity Catalog integration for access control
- **Incremental Development**: Modular operators for easy debugging
- **Production-Ready**: Overwrite mode ensures data freshness

## 🤝 Contributing

Contributions are welcome! Feel free to:
- Report bugs
- Suggest new features
- Submit pull requests
- Share improvements

## 📝 License

This project is open source and available under the MIT License.

## 🔗 Connect

**GitHub**: [Your GitHub Profile]
**LinkedIn**: [Your LinkedIn Profile]

---

**Built with ❤️ using Databricks Lakeflow Designer**
