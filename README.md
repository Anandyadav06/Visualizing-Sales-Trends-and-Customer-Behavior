# Visualizing-Sales-Trends-and-Customer-Behavior

 Step 1: Load & Understand the Data
 import pandas as pd

# Load data
df = pd.read_csv('Walmart_Sales.csv')

# Display the first 5 rows
print(df.head())

# Summary
print(df.info())

# Check for missing values
print(df.isnull().sum())


Data Cleaning & Feature Engineering
# Convert 'Date' to datetime
df['Date'] = pd.to_datetime(df['Date'])

# Create new columns for time-based analysis
df['Month'] = df['Date'].dt.month_name()
df['Day'] = df['Date'].dt.day
df['Weekday'] = df['Date'].dt.day_name()

# Preview changes
print(df[['Date', 'Month', 'Weekday']].head())


Visualizations (Customer Behavior + Sales Trends)
 Monthly Sales Trends
 import matplotlib.pyplot as plt
import seaborn as sns

monthly_sales = df.groupby('Month')['Total'].sum().reindex([
    'January', 'February', 'March'])  # Adjust based on months available

plt.figure(figsize=(10,6))
sns.barplot(x=monthly_sales.index, y=monthly_sales.values)
plt.title('Monthly Sales')
plt.ylabel('Total Sales')
plt.show()


Sales by Gender
sns.boxplot(data=df, x='Gender', y='Total')
plt.title('Sales Distribution by Gender')
plt.show()


City-wise Sales
city_sales = df.groupby('City')['Total'].sum().sort_values()

city_sales.plot(kind='barh', color='skyblue', figsize=(8,5), title='Sales by City')
plt.xlabel('Total Sales')
plt.show()


 Sales by Product Line
sns.barplot(data=df, x='Product line', y='Total', estimator=sum)
plt.xticks(rotation=45)
plt.title('Sales by Product Line')
plt.show()


Sales by Day of Week
weekday_sales = df.groupby('Weekday')['Total'].sum().reindex([
    'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday', 'Sunday'])

weekday_sales.plot(kind='bar', title='Sales by Day of Week', color='orange')
plt.ylabel('Total Sales')
plt.show()
