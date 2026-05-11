Data Cleaning in Excel

This repository contains files with cleaned data. Below are the descriptions of the actions performed for each dataset.
---

📁 20260319 inventory

1. **Table creation:** Preparation of the basic data structure.
2. `warehouse_country` column:
   * Standardizing country names.
   * Adapting data to a single, consistent language.
3. `last_stock_update` column:
   * Validating and standardizing the date format.
   * Removing empty cells (missing data).
   * Removing cells containing errors (e.g., "not_a_date").
   * Removing unrealistic dates (e.g., "2024-13-40").
   * Treating dates in "YYYY-MM" format as the first day of the month.

---

📁 20260320 products

**Data size:** ~2500 rows

1. **Table creation:** Preparation of the basic data structure.
2. **Splitting data** into columns.
3. **Creating a table** to facilitate further analysis.
4. **Price formatting:** Changing the dot to a comma and adding the appropriate currency.
5. **Date cleaning:** Removing invalid dates like "2024-13-40" or incomplete dates "2017-05" (total of **7 items**).
6. **Removing missing values and errors:** Removing empty cells and "not_a_date" entries (total of **97 items**).

---

📁 20260508 sales_orders

Tool: Excel Power Query
Data scope: ~260,000 rows

### 1. order_id column
* Data type: Changed to Text
* Text cleaning: Applied the Trim operation, removing hidden spaces.
* Filtering: Removed empty rows (null).

### 2. customer_id column
* Changed to Text 
* Text cleaning: Applied the Trim operation.

### 3. order_date column
* Converted to Date.
* Error cleaning: Applied the Remove Errors function to eliminate rows with corrupted or illogical date entries that could not be transformed.

### 4. country column
* Applied the Trim operation.
* Forced UPPERCASE / Capitalize Each Word format, standardizing the entries.
* Standardizing country names e.g., PL -> POLAND

### 5. product_id column
* Changed to Text.
* Applied the Trim operation.
* Excluded empty values (null), removing system errors (orders without an assigned product).

### 6. quantity column
* Set to Whole Number.
* Unchecked the value 0, leaving only correct transactions (elimination of errors and returns).
* Removing unnatural orders: Identified several transactions for exactly 608 units of a product. After inspecting these rows, this was deemed an error (so-called garbage data). This specific number was filtered out to avoid artificially inflating our sales results.

### 7. unit_price column
* Replaced dots (.) with commas (,) to adapt the data to Polish regional settings and avoid conversion errors.
* Converted to Decimal Number.
* Removed records with a price of 0.

### 8. discount column
* Replaced dots with commas.
* Converted to Decimal Number.
* Replaced empty cells (null) with the value 0. A business assumption was made that a missing entry means no discount was applied, which prepared the column for safe mathematical operations.

### 9. status column
* Applied the Trim operation.
* Used the Capitalize Each Word option, standardizing the entries (e.g., "completed" and "Completed").
* Reduced 6 naming variants to 3 standardized statuses using the Replace Values function: Complete and Done -> Completed, Ship -> Shipped.
* Unified synonyms for the Cancelled status.
