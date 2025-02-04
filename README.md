# Chipotle Dataset Analysis

## Overview
This project analyzes the Chipotle dataset, which contains information about orders placed at Chipotle restaurants. The dataset is used to perform various filtering, sorting, and aggregation operations using Pandas.

## Dataset Source
The dataset is available at:
[Chipotle Dataset](https://raw.githubusercontent.com/justmarkham/DAT8/master/data/chipotle.tsv)

## Prerequisites
Ensure you have the following Python libraries installed before running the project:

```bash
pip install pandas numpy
```

## Steps Performed

### Step 1: Import the necessary libraries
```python
import pandas as pd
import numpy as np
```

### Step 2: Load the dataset
```python
df = pd.read_csv('https://raw.githubusercontent.com/justmarkham/DAT8/master/data/chipotle.tsv', sep="\t")
```

### Step 3: Assign it to a variable
```python
chipo = df
```

### Step 4: Count of products costing more than $10
```python
chipo['item_price'] = chipo['item_price'].str.replace('$', '').astype(float)
num_expensive_items = chipo[chipo['item_price'] > 10.00].shape[0]
print(num_expensive_items)  # Output: 1130
```

### Step 5: Display item names and prices
```python
chipo[['item_name', 'item_price']]
```

### Step 6: Sort items by name
```python
sorted_chipo = chipo.sort_values(by='item_name')
```

### Step 7: Quantity of the most expensive item ordered
```python
max_price = chipo['item_price'].max()
max_price_quantity = chipo[chipo['item_price'] == max_price]['quantity']
print(max_price_quantity)
```

### Step 8: Count of Veggie Salad Bowl orders
```python
veggie_salad_count = chipo[chipo['item_name'] == 'Veggie Salad Bowl']['item_name'].count()
print(veggie_salad_count)  # Output: 18
```

### Step 9: Count of orders with more than one Canned Soda
```python
num_canned_soda = sum(chipo[chipo['item_name'] == 'Canned Soda']['quantity'] > 1)
print(num_canned_soda)  # Output: 20
```

### Step 10: Order ID with the highest total price
```python
highest_order_id = sum(chipo[chipo['item_price'] == chipo['item_price'].max()]['order_id'])
print(highest_order_id)  # Output: 1443
```

### Step 11: Number of orders where at least one item was ordered multiple times
```python
orders_with_multiple_items = chipo[chipo['quantity'] > 1].shape[0]
print(orders_with_multiple_items)  # Output: 267
```

### Step 12: Billing Report
Create a billing report with the total bill and apply a 5% discount for orders above $50.
```python
chipo['Total_Price'] = chipo['quantity'] * chipo['item_price']
total_bill_df = chipo.groupby('order_id')['Total_Price'].sum().reset_index()
total_bill_df.columns = ['Order_Id', 'Total_Bill']

total_bill_df['Total Bill After Discount'] = total_bill_df['Total_Bill'].apply(
    lambda x: x * 0.95 if x > 50 else x
)

print(total_bill_df)
```

### Expected Output (First Few Rows)
```
   Order_Id  Total_Bill  Total Bill After Discount
0        1       11.56                      11.56
1        2       33.96                      33.96
2        3       12.67                      12.67
3        4       21.00                      21.00
4        5       13.70                      13.70
```

## Conclusion
This project provides insights into Chipotle's sales data using Python and Pandas. Key takeaways include:
- Filtering and sorting data efficiently.
- Aggregating order details and calculating statistics.
- Creating a billing report with discounts.


