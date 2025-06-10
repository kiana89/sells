# City-Based Sales and Product Analysis

This project performs data analysis on customer orders and product information using **Python**, with the help of **Pandas** and **Matplotlib** libraries. The goal is to extract insights into product performance, city-based revenue distribution, and seasonal income trends.

## Data Sources

- `orders.csv`: Includes order details such as quantity, gross amount, finalization date, and city name.
- `product.xlsx`: Contains product metadata like product ID and product title.

---

## Part 1: Top & Bottom Selling Products Per City

### Description

This part joins order and product data using product IDs and then calculates the total number of items sold per product in each city. For every city, the **top 3 best-selling** and **bottom 3 least-selling** products are identified.

### Key Code Snippet

```python
grouped = merged_df.groupby(['city_name_fa', 'ID_Item', 'product_title_fa'])['Quantity_item'].sum().reset_index()
result = grouped.groupby('city_name_fa').apply(top_bottom_products).reset_index(drop=True)
````

### Sample Output

```
  city_name_fa  ID_Item    product_title_fa          Quantity_item
0        Tehran      101    Premium Tarom Rice           253
1        Tehran      203    Golden Frying Oil            198
2        Tehran      110    700g Macaroni                182
3        Tehran      301    Raisins                        5
4        Tehran      145    1g Saffron                     7
5        Tehran      404    Canned Tuna                    9
```

---

## 💵 Part 2: Cities with Highest and Lowest Revenue

### Description

This part calculates the total gross order amount (`Amount_Gross_Order`) per city and identifies the city with the **highest** and **lowest** revenue.

### Key Code Snippet

```python
city_revenue = orders_df.groupby('city_name_fa')['Amount_Gross_Order'].sum().reset_index()
max_city = city_revenue.loc[city_revenue['Amount_Gross_Order'].idxmax()]
min_city = city_revenue.loc[city_revenue['Amount_Gross_Order'].idxmin()]
```

### Sample Output

```
The highest income city:
city_name_fa           Tehran
Amount_Gross_Order     58,792,350.0

The lowest income city:
city_name_fa           Semnan
Amount_Gross_Order     1,782,340.0
```

---

## 📈 Part 3: Seasonal Revenue Analysis by City

### Description

In this part, the finalization date of each order is converted to a quarter period (e.g., Q1, Q2, ...). The total revenue for each city in each quarter is calculated and visualized using a line chart to detect seasonal trends.

### Key Code Snippet

```python
orders_df['quarter'] = orders_df['DateTime_CartFinalize'].dt.to_period('Q')
quarterly = orders_df.groupby(['city_name_fa', 'quarter'])['Amount_Gross_Order'].sum().reset_index()
```

### Sample Output (Chart)

A **line chart** showing the quarterly income for each city:

* **X-axis**: Quarters (`2023Q1`, `2023Q2`, ...)
* **Y-axis**: Gross revenue
* **Each Line**: Represents one city

![Quarterly Income Chart](https://your-image-link.com/quarterly-income-example.png)

## 🛠️ Libraries Used

* `pandas` — data manipulation and aggregation
* `matplotlib` — visualization
* File formats: CSV and Excel

---

## ▶️ How to Run

1. Place `orders.csv` and `product.xlsx` in the root directory of the project.
2. Run the Python scripts using Jupyter Notebook or any Python IDE.
3. Ensure `matplotlib` is installed to view the chart.

---

## 📌 Summary

This project provides a data-driven approach to:

* Discover top and bottom performing products per city
* Identify cities with extreme revenue metrics
* Visualize city-wise seasonal income trends
