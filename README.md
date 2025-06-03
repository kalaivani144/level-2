# LEVEL 2
TASK 1

### ✅ Full Analysis & Visualizations Code

```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Load the dataset
file_path = "Dataset  (2).csv"  # Make sure the CSV is in the same folder
df = pd.read_csv(file_path)

# Set style
sns.set(style="whitegrid")

# -------------------------------
# 1. Distribution of Aggregate Ratings
# -------------------------------
rating_counts = df['Aggregate rating'].value_counts().sort_index()

plt.figure(figsize=(10, 6))
sns.barplot(x=rating_counts.index, y=rating_counts.values, palette="viridis")
plt.title('Distribution of Aggregate Ratings')
plt.xlabel('Aggregate Rating')
plt.ylabel('Number of Restaurants')
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()

# -------------------------------
# 2. Pie Chart: Rating Text Distribution (Excl. 0.0)
# -------------------------------
rating_text_counts = df[df['Aggregate rating'] > 0]['Rating text'].value_counts()

plt.figure(figsize=(8, 8))
plt.pie(rating_text_counts, labels=rating_text_counts.index, autopct='%1.1f%%', startangle=140, colors=sns.color_palette("Set3"))
plt.title('Distribution of Rating Categories (Excluding 0.0)')
plt.axis('equal')
plt.tight_layout()
plt.show()

# -------------------------------
# 3. Votes vs. Aggregate Rating (Boxplot)
# -------------------------------
plt.figure(figsize=(10, 6))
sns.boxplot(x='Aggregate rating', y='Votes', data=df[df['Votes'] > 0], palette="coolwarm")
plt.title('Votes Distribution per Aggregate Rating')
plt.xlabel('Aggregate Rating')
plt.ylabel('Votes')
plt.tight_layout()
plt.show()

# -------------------------------
# Summary Output
# -------------------------------
most_common_rating = rating_counts.idxmax()
most_common_count = rating_counts.max()
average_votes = df['Votes'].mean()

print(f"✅ Most common rating: {most_common_rating} (Count: {most_common_count})")
print(f"✅ Average number of votes: {average_votes:.2f}")
```

---

### 🖼️ What You'll See in Spyder:

1. 📊 **Bar chart**: Distribution of rating values (0.0–5.0).
2. 🥧 **Pie chart**: Percentage of each rating text like "Excellent", "Good", etc.
3. 📦 **Boxplot**: How the number of votes varies across different rating scores.
4. 🖨️ **Console print**:

   ```
   ✅ Most common rating: 0.0 (Count: 2148)
   ✅ Average number of votes: 156.91
   ```
![lvl 2   task 1(aggregate rating)](https://github.com/user-attachments/assets/0ff8dd4d-1d85-44f5-82b5-2e8d3363893d)
![lvl2 task 1(voting)](https://github.com/user-attachments/assets/1d732c3e-600a-45f5-9ad4-c7e74b82ae8f)


TASK 2

### ✅ **Code to Analyze Cuisine Combinations and Ratings**

```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Load dataset
file_path = "Dataset  (2).csv"
df = pd.read_csv(file_path)

# Drop rows with missing cuisines
df = df.dropna(subset=['Cuisines'])

# Task 1: Top 10 most common cuisine combinations
top_combinations = df['Cuisines'].value_counts().head(10)
print("✅ Top 10 Most Common Cuisine Combinations:")
print(top_combinations)

# Task 2: Average rating for each of these combinations
top_combo_list = top_combinations.index.tolist()
filtered = df[df['Cuisines'].isin(top_combo_list)]
avg_ratings = filtered.groupby('Cuisines')['Aggregate rating'].mean().sort_values(ascending=False)
print("\n✅ Average Ratings of Top Cuisine Combinations:")
print(avg_ratings)

# Visualization 1: Bar plot of most common combinations
plt.figure(figsize=(10, 6))
sns.barplot(x=top_combinations.values, y=top_combinations.index, palette="magma")
plt.title('Top 10 Most Common Cuisine Combinations')
plt.xlabel('Number of Restaurants')
plt.ylabel('Cuisine Combination')
plt.tight_layout()
plt.show()

# Visualization 2: Bar plot of average ratings
plt.figure(figsize=(10, 6))
sns.barplot(x=avg_ratings.values, y=avg_ratings.index, palette="viridis")
plt.title('Average Ratings for Top Cuisine Combinations')
plt.xlabel('Average Rating')
plt.ylabel('Cuisine Combination')
plt.xlim(0, 5)
plt.tight_layout()
plt.show()
```

---

### 🖼️ Output:

1. A bar chart of the **top 10 most common cuisine combos**.
2. A second chart comparing their **average ratings**.
3. Console tables with both counts and average ratings.
![lvl2 task 2(combination 1)](https://github.com/user-attachments/assets/609e8fc2-f08f-4951-ad07-3dbb1dd01e27)
![lvl2 task 2(combination](https://github.com/user-attachments/assets/27e8cdd9-3277-4684-9228-0f910e28e6fa)

TASK 3
### ✅ Static Geographic Visualization + City-wise Breakdown 

```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Load dataset
file_path = "Dataset  (2).csv"
df = pd.read_csv(file_path)

# Drop missing values in latitude, longitude, and city
df_geo = df.dropna(subset=['Latitude', 'Longitude', 'City'])

# ----------------------------------
# 1. Static Scatter Plot of Locations
# ----------------------------------
plt.figure(figsize=(10, 6))
sns.scatterplot(data=df_geo, x='Longitude', y='Latitude', hue='City', palette='tab10', s=20, alpha=0.7, legend=False)
plt.title("Restaurant Locations by City")
plt.xlabel("Longitude")
plt.ylabel("Latitude")
plt.grid(True)
plt.tight_layout()
plt.show()

# ----------------------------------
# 2. City-wise Restaurant Count
# ----------------------------------
city_counts = df_geo['City'].value_counts().head(10)
print("✅ Top 10 Cities by Number of Restaurants:")
print(city_counts)

# ----------------------------------
# 3. Bar Plot for Top 10 Cities
# ----------------------------------
plt.figure(figsize=(10, 6))
sns.barplot(x=city_counts.values, y=city_counts.index, palette="crest")
plt.title("Top 10 Cities with Most Restaurants")
plt.xlabel("Number of Restaurants")
plt.ylabel("City")
plt.tight_layout()
plt.show()
```

---

### 🖼️ What You'll See:

1. **Scatter plot** of restaurant locations by `Latitude` and `Longitude`, color-coded by city.
2. **Console output** listing top 10 cities with the most restaurants.
3. **Bar chart** showing those top 10 cities visually.

---
![lvl2 task3(geographical)](https://github.com/user-attachments/assets/05d8f573-eacb-4a5b-b419-a95dc533fa01)
![lvl2 task3(geographical1)](https://github.com/user-attachments/assets/6b235bfe-50f0-409e-ae39-11d8db4c73df)

TASK 4
### 🧠 Complete Spyder-Ready Code for Restaurant Chain Analysis with Cities and Cuisines:

 It includes:

* ✅ Identifying **restaurant chains**
* 📊 Analyzing their **average ratings** and **average votes**
* 🌍 Adding **city count** (how many cities a chain is in)
* 🍽️ Listing **common cuisines per chain**

---



```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Load dataset
file_path = "Dataset  (2).csv"
df = pd.read_csv(file_path)

# Step 1: Identify restaurant chains (appear more than once)
chain_counts = df['Restaurant Name'].value_counts()
chain_names = chain_counts[chain_counts > 1].index
df_chains = df[df['Restaurant Name'].isin(chain_names)]

# Step 2: Analyze each chain: average rating, votes, number of outlets, city count, common cuisines
chain_summary = df_chains.groupby('Restaurant Name').agg({
    'Aggregate rating': 'mean',
    'Votes': 'mean',
    'City': pd.Series.nunique,
    'Restaurant Name': 'count',
    'Cuisines': lambda x: ', '.join(pd.Series.mode(x)[:1])  # Most common cuisine
}).rename(columns={
    'Aggregate rating': 'Average Rating',
    'Votes': 'Average Votes',
    'City': 'City Count',
    'Restaurant Name': 'Outlets',
    'Cuisines': 'Common Cuisine'
}).sort_values(by='Outlets', ascending=False)

# Show top 10 chains
top_chains = chain_summary.head(10)
print("✅ Top 10 Restaurant Chains with City and Cuisine Breakdown:")
print(top_chains)

# Step 3: Visualization - Ratings and Votes of Top Chains
plt.figure(figsize=(10, 6))
sns.barplot(x='Average Rating', y=top_chains.index, data=top_chains, palette='Blues_r')
plt.title("Average Rating of Top 10 Restaurant Chains")
plt.xlabel("Average Rating")
plt.ylabel("Restaurant Chain")
plt.xlim(0, 5)
plt.tight_layout()
plt.show()

plt.figure(figsize=(10, 6))
sns.barplot(x='Average Votes', y=top_chains.index, data=top_chains, palette='Oranges_r')
plt.title("Average Votes of Top 10 Restaurant Chains")
plt.xlabel("Average Votes")
plt.ylabel("Restaurant Chain")
plt.tight_layout()
plt.show()
```

---

### 🖼️ Output Summary:

* Console table with:

  * Average Rating
  * Average Votes
  * Number of Outlets
  * City Coverage
  * Most Common Cuisine Style
* Two **bar plots**:

  1. 📊 **Average Rating** by Chain
  2. ⭐ **Average Votes** by Chain

---
![lvl2 task4(restaurent chains)](https://github.com/user-attachments/assets/55520d24-039b-4711-a2b4-d8c4bdf6b29c)
![lvl2 task4(restaurent chains1)](https://github.com/user-attachments/assets/c7f2f91c-74c5-48d0-a0c9-4c24cee980da)




