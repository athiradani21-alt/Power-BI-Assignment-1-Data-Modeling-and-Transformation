# Power-BI-Assignment-1-Data-Modeling-and-Transformation
## Assigment Overview:

This repository contains the Power BI implementation for analyzing e-commerce sales data. The project covers the end-to-end data preparation lifecycle, including multi-source data ingestion, Power Query  transformations, quality checks for missing/duplicate values, custom column creation, table merges, aggregations, and relational data modeling.Moreover the raw data is given above.

### Dataset Provided:
* List of Orders
* Order Details
* Sales target

#### Implementation:

##### 1.Data importation:

Launch Power BI Desktop and select Get Data and go to Text/CSV.

Load the following source files:
* List of Orders.csv
* Order Details.csv
* Sales target.csv

Click Transform Data to open the Power Query Editor.
##### 2. Data Transformation 
* Select the List of Orders query.

* Go to Home ,then go to Keep Rows $\rightarrow$ Keep Top Rows.

* Set Number of rows to 500.
  
###### Data Type Configuration:

* In List of Orders, set Order Date data type to Date.

* In Order Details, set Amount data type to Fixed Decimal Number .

* In Sales target, set Target data type to Fixed Decimal Number.

###### Text Standardization:

* Select the CustomerName column in List of Orders.

* Go to Format > Capitalize Each Word (Proper Case)

* Column Merging:Multi-select the City and State columns in List of Orders .

* Go to Add Column > Merge Columns.

* Set Separator to Custom > type.

* Name the new column: Location .Custom M Calculation (Profit Margin):Go to Add Column > Custom Column.Name:
   Profit MarginFormula: Profit/Amount

* After that, Set the Data type to %.

###### Conditional Column Logic 

* Go to Add Column > Conditional Column>Column Name: Profit Status

* Set the rules:If Profit is less than 0 > Output: Loss

* Else If Profit equals 0 >Output: Break-Even

* Else > Output: Profit

##### 3. Merging Tables (Joins)

* In Power Query Editor, go to Home > Merge Queries > Merge Queries as New.

* Primary Table: List of Orders

* Secondary Table: Order Details

* Join Column: Select Order ID in both table previews.

* Join Kind: Left Outer (all from first, matching from second).

* Rename the newly created query to Orders Data.

* Expand the merged Order Details column to extract relevant transactional fields (Category, Sub-Category, Profit, Amount).

##### 4. Handling Missing Values

* Applied column profiling to inspect empty/null values across text and numerical fields.

* Filtered out rows with null keys (Order ID) to preserve relational integrity.

###### Handling Duplicate Rows:

* Highlighted key identity columns (Order ID / Order Details key pairs).

* Applied Home > Remove Rows > Remove Duplicates where duplicate entries violated primary key uniqueness.

##### 5. Sorting, Filtering & Aggregations

* In Orders Data, sorted Order Date in Descending order to prioritize recent transactions.

* Applied a text filter on State (e.g., State = "Tamil Nadu") for focused regional evaluation.

###### Query Duplication & Group-By Operations

* Right-click Order Details > Duplicate

* Go to Transform > Group By (Advanced):Group by: Category, Sub-CategoryAggregations: Count of Order ID (Count Rows), Average Profit (Average of Profit), Total Amount (Sum of Amount).

###### Sales Target Aggregation:

* Right-click Sales target > Duplicate.

* Extract  Group by Month of Order Date > Aggregate Total Target Amount (Sum of Target).

##### 6. Data Modeling
* Click Close & Apply to load transformed tables into the Data Model.

* Navigate to the Model View.

* Establish active relationships:List of Orders (Order ID) $\leftrightarrow$ Order Details (Order ID) — 1-to-Many

*  Order Details (Category) > Sales target (Category) — Many-to-1 

