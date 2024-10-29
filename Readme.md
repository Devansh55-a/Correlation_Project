
# Correlation analysis Project

## Project Overview

This project explores a dataset of movies to uncover patterns and relationships between various attributes such as budget, gross revenue, genre, and other key features. Through data preprocessing, correlation analysis, and visualization, this project aims to extract meaningful insights and showcase skills critical for data analyst roles.

### Project Showcase for Portfolio
By showcasing this project, I demonstrate proficiency in:

- Data Preparation: Handling missing values, duplicates, and categorical data transformation.
- Exploratory Data Analysis: Creating meaningful visualizations to uncover data patterns.
- Correlation Analysis: Identifying impactful relationships among movie attributes.

## Technologies and Libraries Used
- Python: Primary language for data analysis.
- Pandas: Data manipulation and analysis.
- Numpy: Numerical operations.
- Seaborn & Matplotlib: Data visualization for creating insightful plots.

### Data Preprocessing
- Loading the Dataset: The movie dataset is loaded and examined for any structural issues.
- Handling Missing Values: Each column is analyzed to calculate the percentage of missing values, helping to decide whether to impute or drop.
- Removing Duplicates: To ensure data integrity, duplicate records are removed.
- Encoding Categorical Variables: Categorical data (e.g., company, genre) is transformed into numeric form for analysis.
```
# Loading and examining the data
df = pd.read_csv('movies.csv')

# Checking missing values for each column
for col in df.columns:
    pct_missing = np.mean(df[col].isnull())
    print(f'{col} - {round(pct_missing*100, 2)}%')

# Removing duplicates
df = df.drop_duplicates()
```


### Exploratory Data Analysis (EDA)
- Scatter Plot: Budget vs. Gross Revenue
We start by visualizing the relationship between a movie's budget and its gross revenue to understand if a higher budget correlates with higher earnings.
```
plt.scatter(x=df['budget'], y=df['gross'], alpha=0.5)
plt.title('Budget vs Gross Earnings')
plt.xlabel('Gross Earnings')
plt.ylabel('Budget for Film')
plt.show()
```
- Top Revenue-Generating Companies
By aggregating gross earnings by company, we identify the top 15 companies based on their gross revenue, adding valuable business context to the analysis.
```
CompanyGrossSum = df.groupby('company')[["gross"]].sum()
CompanyGrossSumSorted = CompanyGrossSum.sort_values('gross', ascending=False)[:15]
print(CompanyGrossSumSorted)
```

### Correlation Analysis
The correlation matrix is used to visualize the relationships between numeric variables like budget, gross, score, and votes.
#### Correlation matrix for numeric columns
```
correlation_matrix = df.corr(method='pearson')
sns.heatmap(correlation_matrix, annot=True)
plt.title("Correlation Matrix for Numeric Features")
plt.show()
```
#### Factorizing Categorical Variables
For categorical columns, factorization assigns numeric values to each unique category, enabling correlation analysis across all features, not just numeric ones.
```
 Applying factorization to categorical variables
df_factorized = df.apply(lambda x: x.factorize()[0] if x.dtype == 'object' else x)
correlation_matrix = df_factorized.corr(method='pearson')
sns.heatmap(correlation_matrix, annot=True)
plt.title("Correlation Matrix for Movies (Including Categorical Data)")
plt.show()
```

### Key Findings and Insights
- Budget and Gross: A strong positive correlation was observed, indicating that higher-budget movies tend to earn more in gross revenue.
- Score and Votes: High correlation, suggesting that movies rated well often receive more votes, possibly due to higher engagement.
- Company Performance: Certain companies consistently generate high revenue, emphasizing the influence of production companies on movie success.

### Conclusion
This project highlights essential data analysis techniques, from data cleaning and transformation to in-depth exploratory analysis and visualization. Through correlation analysis, we identified critical factors that potentially influence a movie's success, offering valuable insights for stakeholders in the movie production industry.
