# DATA SOURCES 


## Details 

#  _Olist Products Dataset_ 
(`olist_products_dataset.csv`)_ with 610 records were missing category name and all descriptive metadata fields. 

So, i had doing some cleaning method for this. For example, fill missing values with 'Uncategorized'  
in `product_category_name`, why? instead of leaving them blank, this give us a clear label. 

```python
df_product['product_category_name'] = df_product['product_category_name'].fillna('Uncategorized')
```
 
 Next to i filled missing value with 0 in these features: 
- `product_name_lenght`
- `product_description_lenght`
- `product_photos_qty` 

These data represent counts or lengths that logically default to zero when information is unavailable. 

```python
cols_to_zero = ['product_name_lenght', 'product_description_lenght', 'product_photos_qty']
df_product[cols_to_zero] = df_product[cols_to_zero].fillna(0)
```
Then complete some features left: 
- `product_weight_g`
- `product_length_cm`
- `product_height_cm`
- `product_width_cm`

Accurate dimensions are essential for calculating shipping costs and logistics. I chose the Median instead of the Average because it’s much more resilient to "outliers". Those rare, extremely large or tiny products that can skew the results. 


---

#  _Olist Geolocation Dataset_ 

In (`olist_geolocation_dataset.csv`), I identified and removed redundant records that were ruinnung the dataset. 





--- 

#  _Olist Orders Dataset_ 

In this dataset, i selected all timestamp columns (e.g., order_purchase_timestamp) and converted them using the Text-to-Columns wizard, strictly defining the format as YMD (Day-Month-Year).

I discovered 8 orders marked as delivered that completely lacked a delivery_date.Since an order cannot be "delivered" without a date, I manually flagged these as `Shipped` base on the `order_delivered_customer_date` and `order_purchase_timestamp`


Before the final, I created a temporary "Logic Flag" column with formula 

```excel
=IF([Delivery Date] < [Purchase Date], "Error", "OK")
```

and it showed few errors then removed it. 

You will see some null value in many column but i did not remove it, because some orders have not delivered yet.


--- 


#  _Olist Order Reviews Dataset_ 

In this high null count dataset, over 87k rows have no review title and 58k have no message.  i already fill these with `No title` and `No comment`. 




--- 


I have good news. After scrubbing the heavy files like Reviews and Locations, I moved on to the final four datasets: Items, Payments, Customers, and Sellers.

To my relief, these files were remarkably clean. I didn't have to perform any complex surgery like I did with the others. Here is my field report on why they are safe to import immediately.

