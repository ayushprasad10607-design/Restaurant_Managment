import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

# ----------------------------
# Restaurant Menu Data
# ----------------------------
menu_data = {
    "Item": ["Veg Pizza", "Chicken Burger", "French Fries", "Cold Drink", "Veg Sandwich"],
    "Price": [200, 150, 90, 50, 120]
}

menu_df = pd.DataFrame(menu_data)
print("\n--- RESTAURANT MENU ---")
print(menu_df)

# ----------------------------
# Customer Orders Data
# ----------------------------
order_data = {
    "Item": ["Veg Pizza", "French Fries", "Veg Pizza", "Cold Drink", "Chicken Burger", "Cold Drink"],
    "Quantity": [1, 2, 1, 3, 2, 1]
}

orders_df = pd.DataFrame(order_data)

# ----------------------------
# Billing Calculation
# ----------------------------
bill_df = pd.merge(orders_df, menu_df, on="Item")
bill_df["Amount"] = bill_df["Price"] * bill_df["Quantity"]

print("\n--- BILL DETAILS ---")
print(bill_df)

# ----------------------------
# Total Bill Amount
# ----------------------------
final_bill = np.sum(bill_df["Amount"])
print("\nTotal Payable Amount: ₹", final_bill)

# ----------------------------
# Sales Summary
# ----------------------------
item_sales = bill_df.groupby("Item")["Quantity"].sum()

print("\n--- ITEM SALES SUMMARY ---")
print(item_sales)

# ----------------------------
# Visualization
# ----------------------------
plt.figure()
item_sales.plot(kind="bar")
plt.title("Restaurant Item Sales Analysis")
plt.xlabel("Food Items")
plt.ylabel("Total Quantity Sold")
plt.tight_layout()
plt.show()
