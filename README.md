Plot 1

import pandas as pd
import matplotlib.pyplot as plt
# Read the CSV file into a DataFrame
df = pd.read_csv('gcar_data.csv')
# Group by brand and count the number of models for each brand
brand_counts = df.groupby('brand')['model'].nunique().
↪sort_values(ascending=False)
# Select the top 10 brands with the most models
top_brands = brand_counts.head(10)
# Plotting
plt.figure(figsize=(10, 6))
top_brands.plot(kind='bar', color='skyblue')
plt.title('Top 10 Car Brands with Most Models')
plt.xlabel('Car Brands')
plt.ylabel('Number of Models')
plt.xticks(rotation=45, ha='right')
plt.tight_layout()
plt.show()


Plot 2


 # Count the number of sales for each year
sales_by_year = df['year'].value_counts()
# Select the top 5 years with the most sales
top_years = sales_by_year.head(5)
# Plotting pie chart
plt.figure(figsize=(8, 8))
plt.pie(top_years, labels=top_years.index, autopct='%1.1f%%', startangle=140)
plt.title('Distribution of Sales by Year')
plt.axis('equal') # Equal aspect ratio ensures that pie is drawn as a circle.
plt.show()
# Creating a table
print("Year\t\tSales")
print("---------------------")
for year, sales in top_years.items():
print(f"{year}\t\t{sales}")



Plot 3


# Group by model and count the number of sales for each model
sales_by_model = df.groupby('model')['year'].count().
↪sort_values(ascending=False)
# Select the top 20 most-selling models
top_models = sales_by_model.head(20)
# Filter the DataFrame to include only the sales data for the top models
top_models_sales = df[df['model'].isin(top_models.index)]
# Group by model and year, and count the number of sales for each year
sales_by_model_year = top_models_sales.groupby(['model', 'year']).size().
↪unstack().fillna(0)
# Plotting
plt.figure(figsize=(12, 8))
for model in sales_by_model_year.index:
plt.plot(sales_by_model_year.columns, sales_by_model_year.loc[model],␣
↪label=model)
plt.title('Sales Trend of Top 20 Most-Selling Models')
plt.xlabel('Year')
plt.ylabel('Number of Sales')
plt.legend(loc='upper left', bbox_to_anchor=(1, 1))
plt.xticks(sales_by_model_year.columns, rotation=45, ha='right') # Rotate the␣
↪x-axis labels
plt.grid(True)
plt.tight_layout()
plt.show()


Plot 4



# Create a violin plot
plt.figure(figsize=(12, 8))
sns.violinplot(x='year', y='transmission_type', hue='fuel_type', data=df,␣
↪split=True, inner="quartile")
plt.title('Car Sales Trend by Transmission and Fuel Type')
plt.xlabel('Year')
plt.ylabel('Transmission Type')
plt.legend(title='Fuel Type', loc='upper left', bbox_to_anchor=(1, 1))
plt.xticks(rotation=45) # Rotate the x-axis labels by 45 degrees
plt.tight_layout()
plt.show()



