# Logistics Data Analyst Internship - Week 1

## Strategic Planning and Data Exploration in Logistics

### Project Overview
End-to-end strategic planning and predictive analytics workflow to optimize supply chain delivery timelines and last-mile logistics performance.

### Core KPIs
- **On-Time Delivery Rate (OTDR)**: Target >= 95%
- **Average Transit Time (ATT)**: Target reduction by 12%
- **Order Fulfillment Cost Per Unit (OFPU)**: Cost optimization via route clustering

### Python Exploration Script
```python
import numpy as np
import pandas as pd

# Load logistics data
df = pd.read_csv("logistics_orders.csv")

# Feature engineering
df["actual_transit_days"] = (
    pd.to_datetime(df["order_delivered_customer_date"])
    - pd.to_datetime(df["order_delivered_carrier_date"])
).dt.total_seconds() / 86400.0

df["is_delayed"] = np.where(
    df["order_delivered_customer_date"] > df["order_estimated_delivery_date"],
    1,
    0,
)

# KPIs
otdr = ((df["is_delayed"] == 0).sum() / len(df)) * 100
print(f"OTDR: {otdr:.2f}%")
