# Project_AC_data_anaytics
import pandas as pd
df=pd.read_csv("ac2.csv")

df

df.info()

df.isnull().sum()

df["Model"].mode()

df["Model"]=df["Model"].fillna(value="2023 Model")

df["Model"].isnull().sum()

df["Stars"].mode()

df["Stars"]=df["Stars"].fillna(value="3 star")

df["Stars"].isnull().sum()

df["Weights"].mode()

df["Weights"]=df["Weights"].fillna(value="1.5 Ton")

df["Weights"].isnull().sum()

df["PowerUsage"].mean()

df["PowerUsage"].median()

df["PowerUsage"]=df["PowerUsage"].fillna(value="866.495")

df["PowerUsage"].isnull().sum()

df["PowerUsage"]=df["PowerUsage"].astype("float")

df.info()

df["Rating"].mode()

df["Rating"]=df["Rating"].fillna(value="4.2")

df["Rating"]=df["Rating"].replace("[^\d+]","",regex=True).astype("float")

df.info()

df["Price"].mode()

df["Price"]=df["Price"].fillna(value=32990)

df["Price"]=df["Price"].replace("[^\d+]","",regex=True).astype("int")

df.info()

df["RoomSize"].mode()

df["RoomSize"]=df["RoomSize"].fillna(value="150 sqft")

df.info()

df

df.isnull().sum()

df.info()

# Univariate

import matplotlib.pyplot as plt
import seaborn as sns

### Q1. Counting Brand names of AC

df["Brand"].value_counts()

## Catergorical

plt.xlabel("Brand")
plt.title("Brand distribution")
sns.countplot(x="Brand",data=df,palette="viridis")
plt.xticks(rotation=100)
plt.show()

## Q2.Print price distribution

df["Price"].value_counts()

## Countinous

sns.histplot(data=df, bins=10, kde=False,color="viridis")
plt.title('Price Distribution Histogram')
plt.xlabel('price')
plt.ylabel('Frequency')

plt.show()

## Bivariate

### Categorical and continous

#### Q3.Get a rating for different brands.

# Group data by brand and calculate the mean rating
brand_rating_mean = df.groupby("Brand")["Rating"].mean().sort_values()


# Plot the data
plt.figure(figsize=(5, 4))
brand_rating_mean.plot(kind="bar")
plt.xlabel("Brand")
plt.ylabel("Mean Rating")
plt.title("Brand Distribution by Mean Rating")
plt.xticks(rotation=100)

# Show the plot
plt.show()

### Continous and continous

#### Q4.Plota Price according to PowerUsage of their distribution

plt.figure(figsize=(8, 6))
sns.regplot(x='PowerUsage', y='Price', data=df, color='blue')
plt.title('Scatter Plot: PowerUsage vs. Price')
plt.xlabel('PowerUsage')
plt.ylabel('Price')

# Show the plot
plt.show()

#### Q5.Calculating a relationship of columns

# Calculate the correlation matrix
correlation_matrix = df.corr()

# Create a correlation heatmap
plt.figure(figsize=(8, 6))
sns.heatmap(correlation_matrix, annot=True, cmap='coolwarm', center=0)
plt.title('Correlation Heatmap')


# Show the plot
plt.show()

### Multivariate

#### Categorical and Countinous

plt.figure(figsize=(10, 6))
sns.barplot(x='Brand', y='PowerUsage', data=df, palette='Set2')
plt.title('Bar Plot: Average Power Usage by Brand')
plt.xlabel('Brand')
plt.ylabel('Power Usage')
plt.xticks(rotation=100)  # Adjust the rotation angle as needed
plt.show()

#### Q5.Getting brands of 5star rating

five_star_df = df[df['Rating'] == 4.0]

# Create a count plot to visualize the brands with 5-star ratings
plt.figure(figsize=(10, 6))
sns.countplot(x='Brand', data=five_star_df, palette='Set2')
plt.title('Count Plot: Brands with 5-Star Ratings')
plt.xlabel('Brand')
plt.ylabel('Count')
plt.xticks(rotation=100)

# Show the plot
plt.show()

#### Categorial and Countinous

#### Q6.Draw a plot for average price and powerusage by brand

plt.figure(figsize=(10, 6))
sns.barplot(x='Brand', y='Price', data=df, ci=None, color='skyblue', label='Price')
sns.barplot(x='Brand', y='PowerUsage', data=df, ci=None, color='green', label='PowerUsage')
plt.title('Average Price and Powerusage Capacity by Brand')
plt.xlabel('Brand')
plt.ylabel('Value')
plt.xticks(rotation=100)
plt.legend()

# Show the plot
plt.show()



