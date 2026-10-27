# 🐼 Python pandas: exploring and cleaning data

**Filtering, cleaning and summarising four datasets with pandas, with charts in Matplotlib and seaborn.**

Four Google Colab notebooks from Week 6 of my bootcamp, covering a small sales table, car fuel economy, penguin measurements with missing values, and GDP per capita for 223 countries and territories. Across the four, I loaded data, filtered and selected it, dealt with missing values and outliers, summarised it by group and charted it.

This builds on the programs in my [Python basics](https://github.com/isobel-hannington/python-basics) repository from earlier in the same week.

## 🔎 At a glance

| | |
|---|---|
| **Tools** | Python 3, pandas, NumPy, Matplotlib, seaborn, Google Colab |
| **Datasets** | A sales table built in code, mpg (234 cars), Palmer penguins (344 penguins) and GDP (nominal) per capita (223 countries and territories), plus a student marks file (35 students) |
| **Bootcamp week** | Week 6 (October 2026), Level 3 Data Technician Skills Bootcamp, Leep Talent |
| **Type** | Course notebooks. The first three teach pandas through worked examples and end with exercises that I completed. The GDP notebook is a guided analysis that I worked through. |
| **Colab links** | [Task 1](https://colab.research.google.com/drive/1QpG9AGITvzolcj2Q5HGzwNDDucIp6Fns?usp=sharing) · [Task 2](https://colab.research.google.com/drive/1OkaoYrETIEQQwl80lXGj9dHoVeyDl8Bo?usp=sharing) · [Task 3](https://colab.research.google.com/drive/1bvXZ8Vp_cpGCjxlsx5qphVxIzRcSMGZ-?usp=sharing) · [Task 4](https://colab.research.google.com/drive/1fun0EuyUbmDeHxVpL-9G4veBi4_Z5FyL?usp=sharing) |

## 💡 Skills demonstrated

**✔️ Loading and exploring**
- `read_csv()` to load data (Tasks 2 to 4), and `to_csv()` and `to_excel()` to export it (Task 1)
- `head()`, `tail()`, `sample()`, `shape`, `info()`, `describe()`, `dtypes`, `unique()` and `value_counts()` to check a dataset before analysing it (every notebook, most fully in the GDP one)

**✔️ Selecting and filtering**
- `.loc` to select and fill a column (Task 1)
- Boolean masks with `str.contains()` (Task 2), combined with `&` (Task 4)
- `nlargest()` and `nsmallest()` to find the top and bottom rows (Tasks 2 and 4)

**✔️ Cleaning**
- `str.replace()` and `astype()` to turn text prices into numbers, and `rename()` for columns (Task 1)
- `isna()`, `dropna()` and `drop()` to find and remove missing values (Task 3)
- `replace()` and `fillna()` to mark and fill gaps that were stored as zeros (Task 4)

**✔️ Summarising**
- `groupby()` with `mean()` and `median()`, and `sort_values()` to rank the results (Task 4)
- `corr()` to check relationships (Tasks 2 and 4) and `quantile()` for the interquartile range (Task 4)

**✔️ Visualising**
- Histograms, a heatmap, bar charts, a scatter plot and box plots with Matplotlib and seaborn (Task 4)

## 📗 Exercises covered

| Notebook | What I did |
|---|---|
| [Task 1: DataFrames](notebooks/day4-task1-pandas-dataframes.ipynb) | Built a sales table, cleaned text prices into numbers, calculated revenue and exported the result to CSV and Excel |
| [Task 2: fuel economy](notebooks/day4-task2-mpg-fuel-economy.ipynb) | Flagged automatic cars, worked out the share of subcompacts, built a weighted fuel economy score and filtered cars above the median |
| [Task 3: missing values](notebooks/day4-task3-penguins-missing-values.ipynb) | Counted missing values by column and by row, then dropped incomplete rows |
| [Task 4: GDP per capita](notebooks/day4-task4-gdp-per-capita.ipynb) | Compared three sources, summarised by region, filled missing IMF figures, drew histograms, a heatmap, bar charts and box plots, and removed outliers with the interquartile range |

## 🗂️ Data

| File | What it is | Used in |
|---|---|---|
| `data/mpg.csv` | Fuel economy for 234 cars from 1999 and 2008: manufacturer, engine size, cylinders, transmission, city and highway miles per gallon, and vehicle class | Task 2 |
| `data/penguins.csv` | Measurements of 344 penguins of three species from the Palmer Archipelago, Antarctica, with some values missing | Task 3 |
| `data/GDP_nominal_per_Capita.xlsx` | GDP per capita in US dollars for 223 countries and territories, with separate estimates from the IMF, World Bank and UN | Task 4 |
| `data/student.xlsx` | A sample class list of 35 students: name, class, mark and gender | A class exercise in Colab (that notebook isn't included here) |

The mpg and penguins files are standard public teaching datasets, and the GDP data is a [Kaggle dataset](https://www.kaggle.com/datasets/rajkumarpandey02/gdp-in-usd-per-capita-income-by-country). To rerun a notebook in Colab, upload its dataset first.

## 🧩 Code highlights

### Selecting with `.loc` and cleaning a text column

![loc and astype](images/code-01-loc-astype-revenue.png)

`.loc` fills the `units_sold` column. Prices arrived as text, such as "$10.99", so `str.replace()` removed the $ sign and `astype(float)` turned them into numbers. The USB A to USB C cable brought in the most revenue: $1,242.

### Filtering with Boolean masks

![Boolean masks](images/code-02-boolean-masks.png)

`str.contains('auto')` marks each car True or False, and adding up the True values counts them: 157 of the 234 cars are automatic. A mask on a fuel economy score, weighted 55% city and 45% highway, keeps the 114 cars above the median.

### Finding and dropping missing values

![Missing values](images/code-04-missing-values-dropna.png)

`isna().sum()` counts the gaps in each column: 11 penguins have no sex recorded and 2 have no body measurements. `dropna()` removes every incomplete row, taking the data from 344 rows to 333.

### Summarising by group

![groupby and sort_values](images/code-05-groupby-sort-values.png)

`groupby("UN_Region")` collapses the countries into regions and `sort_values()` ranks them. Asia and the Americas swap places between the mean and the median, because a few very wealthy countries pull the mean up.

### Filling missing values

![fillna](images/code-06-fillna.png)

Missing IMF estimates were stored as 0. `replace(0, np.nan)` marks them as missing, and `fillna()` fills each one with the average of the World Bank and UN estimates. Monaco now has an IMF figure of $234,316.50.

### Removing outliers with the interquartile range

![IQR outliers](images/code-07-iqr-outliers.png)

The middle half of countries have a UN estimate between $2,039 and $20,740. Anything more than 1.5 times that range above the upper quartile, $48,791.50, counts as an outlier. Filtering with `&` keeps 196 rows and removes 27.

## 📸 Charts from the GDP notebook

**How closely the three sources agree:** correlations between 0.93 and 0.98

![Correlation heatmap](images/gdp-correlation-heatmap.png)

**Spread of the UN estimate.** The points to the right are the outliers removed above.

![Box plot of the UN estimate](images/gdp-un-estimate-boxplot.png)

## 📈 Results

- **Fuel economy:** engine size and cylinders both have a correlation of −0.79 with average mileage. The most economical car is the 1999 Volkswagen New Beetle 1.9 diesel manual, at 35 mpg in town and 44 on the highway.
- **Penguins:** dropping incomplete rows removes 11 of the 344 penguins, about 3% of the data.
- **GDP per capita:** the median IMF estimate is $5,421, but the mean is $15,352. Removing outliers cuts the mean UN estimate from $17,767 to $9,415.
- **Data quality:** `UN_Year` is stored as text because one value carries a footnote marker, `[n 10]2021`.

## 🎓 Key learning outcomes

- Check data types before calculating. Text prices had to become numbers before revenue could be worked out.
- A zero can mean "missing", and treating it as a real value pulls averages down.
- Compare the mean with the median before trusting an average.
- Use a clear rule, such as the interquartile range, to decide what counts as an outlier.

## 🧠 What I'd change

- **A zero isn't always a zero.** For 8 territories the UN figure was also 0, so their filled IMF value is only half their World Bank figure: the Isle of Man shows $43,579 against a World Bank estimate of $87,158. Replacing zeros with blanks in both columns first would fix this.
- **Leave out totals.** The GDP table includes a "World" row, which shows up as its own region in the summaries. Removing it first would keep the comparison to real countries.

## 🛠️ Tools and technologies

- **pandas:** loading, filtering, cleaning and summarising the data
- **NumPy:** `np.nan` to mark missing values
- **Matplotlib and seaborn:** the charts in the GDP notebook
- **Google Colab:** writing and running the notebooks, with comments explaining each step, and sharing them by link

## 📁 Repository contents

| File or folder | What it is |
|---|---|
| `Data_Technician_Workbook_Week_6.docx` | My completed Week 6 workbook, with the Colab link for each notebook |
| `notebooks/` | The four pandas notebooks, downloaded from Colab with their output saved |
| `data/` | The datasets used in the notebooks, plus the student marks file |
| `images/` | Screenshots of code and output from the notebooks, and charts from the GDP notebook |
