PANDAS FOUNDATION

### 🪜 Step‑by‑Step Focus Areas

1. **Loading and Inspecting Data**
   - `pd.read_csv()`, `df.head()`, `df.info()`, `df.describe()`
   - Learn how to quickly peek at your dataset and understand its shape, columns, and types.

2. **Selecting and Filtering**
   - Accessing columns: `df['col']`, `df[['col1','col2']]`
   - Filtering rows: `df[df['col'] > 10]`, `df.query("col == 'value'")`

3. **Cleaning Data**
   - Handling missing values: `df.dropna()`, `df.fillna()`
   - String operations: `.str.strip()`, `.str.lower()`
   - Renaming columns: `df.rename()`

4. **Transforming Data**
   - Creating new columns: `df['new'] = df['old'] * 2`
   - Applying functions: `df['col'].apply(func)`
   - Changing types: `df.astype()`

5. **Aggregating and Grouping**
   - `df.groupby('col').mean()`
   - `df.groupby(['col1','col2']).agg({'col3':'sum'})`

6. **Merging and Joining**
   - `pd.merge(df1, df2, on='key')`
   - `pd.concat([df1, df2])`

7. **Exporting Results**
   - `df.to_csv('clean.csv', index=False)`

---

### 🎯 What to Practice
- Take a messy CSV (like one with inconsistent capitalization, extra spaces, or missing values) and clean it up.
- Try grouping by a category (e.g., customers, products) and calculate totals.
- Merge two datasets together (e.g., customers + orders).

---

### 🚀 Next Steps
Once you’re comfortable with the basics, you can branch into:
- **Visualization** with `matplotlib` or `seaborn`.
- **Time series** handling with pandas’ `DatetimeIndex`.
- **Performance tricks** like `.loc` vs `.iloc`, vectorization, and avoiding loops.

---

👉 My advice: focus first on **loading, cleaning, and filtering**. That’s 80% of real-world data work. Once you can confidently wrangle messy tables, everything else builds naturally.

Do you want me to sketch out a **mini practice project** (like cleaning a customer dataset and analyzing sales) so you can apply these steps in a hands-on way?
