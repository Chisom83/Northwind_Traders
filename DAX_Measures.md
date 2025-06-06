## All DAX Measures used in Power BI for this aanalysis 

### Total Revenue 
```
SUMX(order_details,order_details[quantity] * RELATED(products[unitPrice]) * (1- order_details[discount]))
```

### PYRevenue 
```
VAR PY = CALCULATE([Total Revenue],PREVIOUSYEAR('Calendar'[Date]))
VAR CY = [Total Revenue]
VAR PCT = FORMAT(DIVIDE(CY - PY, PY, 0), "0%")
VAR ARROW_SIGN = IF(CY > PY,"◬", "▽")
RETURN "PY:" & PCT & ARROW_SIGN
```

### Total Orders
```
DISTINCTCOUNT(orders[orderID])
```

### PYOrders 
```
VAR PY = CALCULATE([Total Orders],PREVIOUSYEAR('Calendar'[Date]))
VAR CY = [Total Orders]
VAR PCT = FORMAT(DIVIDE(CY - PY, PY, 0), "0%")
VAR ARROW_SIGN = IF(CY > PY,"◬", "▽")
RETURN "PY:" & PCT & ARROW_SIGN
```

### AOV 
```
AVERAGEX(orders, [Total Revenue])
```

### PYAOV  
```
VAR PY = CALCULATE([AOV],PREVIOUSYEAR('Calendar'[Date]))
VAR CY = [AOV]
VAR PCT = FORMAT(DIVIDE(CY - PY, PY, 0), "0%")
VAR ARROW_SIGN = IF(CY > PY,"◬", "▽")
RETURN "PY:" & PCT & ARROW_SIGN
```

### Average Shipping Time
```
AVERAGEX(orders,orders[shippedDate] - orders[orderDate])
```
### LateDelivery  
```
 CALCULATE(
    COUNTROWS(orders),
    orders[shippedDate] > orders[requiredDate])
```
### OnTimeDelivery 
```
 CALCULATE(
    COUNTROWS(orders),
    orders[shippedDate] <= orders[requiredDate])
```
### Average Freight 
```
AVERAGE(orders[freight])
```
### Switch Product Top/Bottom 
```
{
    ("Top", NAMEOF('DAX Measures'[Product Dynamics Top]), 0),
    ("Bottom", NAMEOF('DAX Measures'[Product Dynamics Bottom]), 1)
}
```
### Top/Bottom Product 
```
GENERATESERIES(1, 10, 1)
```
*The switch Product Top/Bottom was achieved by clicking the modeling tab and then the new parameter then the numeric range, finally seting it up as required.*
