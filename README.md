# 🚢 Titanic Dataset - Exploratory Data Analysis (EDA)

This project presents a detailed **exploratory data analysis (EDA)** of the Titanic dataset using `pandas`, `matplotlib`, and `seaborn`. The goal is to understand survival patterns based on various passenger features such as class, sex, age, title, family size, and embarkation port.

---

## 📁 Dataset

- Source: `train.csv` from the [Titanic Kaggle Competition](https://www.kaggle.com/competitions/titanic)
- Size: 891 rows × 12 columns
- Key Columns:
  - `Survived`: Target variable (0 = No, 1 = Yes)
  - `Pclass`: Ticket class (1 = 1st, 2 = 2nd, 3 = 3rd)
  - `Sex`, `Age`, `Fare`, `Embarked`: Demographic and economic features
  - `SibSp`, `Parch`: Siblings/spouses & parents/children aboard
  - `Name`: Used to extract titles

---

## 🔍 Key EDA Tasks

### 1. **Survival Analysis by Class and Gender**

- Grouped survival rate by `Pclass` and visualized it as percentages.
- Found that higher classes had better survival rates:
  - 1st class: ~63%
  - 2nd class: ~47%
  - 3rd class: ~24%

- Gender had strong predictive power:
  - Female survival rate: ~74%
  - Male survival rate: ~19%

### 2. **Title Extraction and Aggregation**

- Extracted `Title` (Mr, Miss, Mrs, etc.) from the `Name` column using regex.
- Grouped rare titles under `others`.
- Found meaningful survival differences between titles:
  - Miss, Mrs had higher survival
  - Mr had lowest survival

### 3. **Family Size Analysis**

- Created a new `Family` feature: `SibSp + Parch`
- Explored how family size affected survival
- Smaller families (1–3 members) showed higher survival probabilities than singles or very large families.

### 4. **Visualizations**

Used `seaborn` and `matplotlib` to produce:

- 📊 **Barplots** of survival by class, gender, title, family size
- 📈 **Line and box plots** to explore relationships like `Age vs. Survived`, `Fare vs. Pclass`, etc.
- 📦 **Box and violin plots** for distribution checks
- 📉 **Histograms and scatterplots** for feature exploration
- 🟨 **PairGrid** and `df.hist()` for multivariate exploration

### 5. **Missing Value Handling**

- Imputed `Age` using group-wise means (`Sex + Title` combinations).
- Example:
  - Female + Miss → ~21.77
  - Male + Mr → ~32.37

---

## 📊 Insights

- **Women and children (Miss, Master)** had much higher survival rates.
- **1st class passengers** had higher chances of survival than 2nd and 3rd.
- Titles were strongly correlated with age and survival.
- Family presence mattered: being alone or in a very large group reduced survival odds.

---

## 🛠 Technologies Used

- Python 3
- pandas, numpy
- seaborn, matplotlib

---

## 📈 Example Code Snippets

```python
# Extracting title
df["Title"] = df["Name"].str.extract(' ([A-Za-z]+)\.')

# Grouping and visualizing survival rate by title
sns.barplot(data=df, x='Title', y='Survived')

# Creating family size feature
df["Family"] = df["SibSp"] + df["Parch"]
sns.barplot(data=df.groupby("Family")["Survived"].mean().reset_index(), x='Family', y='Survived')
