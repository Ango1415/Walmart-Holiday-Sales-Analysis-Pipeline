![Project Banner](walmartecomm.jpg)

# 📦 Walmart Holiday Sales Analysis Pipeline

## 📝 Description

Walmart is the largest retail chain in the US, with a rapidly growing e-commerce business that reached \$80 billion in sales by the end of 2022 (13% of total sales). One key factor influencing sales is public holidays such as the Super Bowl, Labor Day, Thanksgiving, and Christmas.

This project builds a **data pipeline** to analyze supply and demand around holidays. It uses two data sources:

- **PostgreSQL database:** `grocery_sales` table
- **Parquet file:** `extra_data.parquet` (complementary data)

> **Note:** To simplify this exercise, the merge between the PostgreSQL table and the Parquet file has already been done and is provided as `merge_df.csv`.

---

## 🎯 Objective

- Build an ETL (Extract, Transform, Load) pipeline to combine, clean, transform, and analyze sales data.
- Analyze Walmart's average monthly sales considering holidays, temperature, fuel prices, unemployment, and promotions.
- Save the results as CSV files for future analysis.

---

## ⚙️ Data Structure

** table:**

| Column         | Description                |
| -------------- | -------------------------- |
| `index`        | Unique row ID              |
| `Store_ID`     | Store number               |
| `Date`         | Sales week                 |
| `Weekly_Sales` | Weekly sales for the store |

** file:**

| Column         | Description                                          |
| -------------- | ---------------------------------------------------- |
| `IsHoliday`    | 1 if the week includes a public holiday, 0 otherwise |
| `Temperature`  | Temperature on the sale day                          |
| `Fuel_Price`   | Regional fuel price                                  |
| `CPI`          | Consumer Price Index                                 |
| `Unemployment` | Unemployment rate                                    |
| `MarkDown1-4`  | Promotional markdowns                                |
| `Dept`         | Store department number                              |
| `Size`         | Store size                                           |
| `Type`         | Store type (based on size)                           |

---

## 🔄 Pipeline Flow

1. **Extract:**

   - Extract data from `grocery_sales` using SQL.
   - Read `extra_data.parquet` with `pandas`.

2. **Transform:**

   - Merge both datasets (\*already done, see `merge_df.csv`).
   - Fill missing numerical values.
   - Extract the month from the `Date` column and create a `Month` column.
   - Keep rows where `Weekly_Sales` > \$10,000.
   - Keep only necessary columns: `Store_ID`, `Month`, `Dept`, `IsHoliday`, `Weekly_Sales`, `CPI`, `Unemployment`.

3. **Aggregate:**

   - Calculate average weekly sales per month using `groupby` and `agg`.

4. **Load:**

   - Save `clean_data` and `agg_data` as `.csv` files without index.
   - Validate that the files were created successfully.

---

## 🧩 Functions Structure

| Function                                   | Description                                 |
| ------------------------------------------ | ------------------------------------------- |
| `transform(merged_df)`                     | Cleans and transforms the merged DataFrame. |
| `avg_weekly_sales_per_month(clean_data)`   | Calculates average monthly sales.           |
| `load(clean_data, agg_data, path1, path2)` | Saves the resulting CSV files.              |
| `validation()`                             | Checks that the CSV files exist.            |

---

## 🧪 Requirements

- **Python 3.8+**
- **Libraries:**
  - `pandas`

---

## 👤 Author

[**DataCamp**](https://app.datacamp.com/)

---

## 📄 License

This project is released under the **MIT License**. See `LICENSE` for details.

