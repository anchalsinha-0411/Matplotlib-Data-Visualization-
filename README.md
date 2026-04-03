# Matplotlib-Data-Visualization

# Matplotlib and Pandas Data Visualization

This Colab notebook provides a comprehensive introduction to data visualization using `matplotlib` and `pandas` in Python. It covers various types of plots, customization options, and integration with pandas DataFrames for exploring and presenting data.

## Table of Contents
- [Setup and Installation](#setup-and-installation)
- [Matplotlib Basics](#matplotlib-basics)
- [Scatter Plots](#scatter-plots)
- [Line Plots](#line-plots)
- [Histograms](#histograms)
- [Bar Charts](#bar-charts)
- [Box Plots](#box-plots)
- [Pandas Integration](#pandas-integration)
- [Data Source](#data-source)

## Setup and Installation
To run this notebook, you'll need Python and the following libraries:
- `matplotlib`
- `numpy`
- `pandas`

You can install them using pip:
```bash
pip install matplotlib numpy pandas
```

If running in Google Colab, these libraries are typically pre-installed.

## Matplotlib Basics
This section covers the fundamental usage of `matplotlib.pyplot` for creating simple plots, setting axis limits, and customizing plot elements.

```python
import matplotlib.pyplot as plt

plt.plot(1, 2) # Simple plot
plt.plot(3, 2, 'x') # Plot with marker
plt.plot(3, 2, linestyle='-', color='green') # Styled plot
plt.show()

# Customizing axes
plt.figure()
plt.plot(3, 2, 'x')
ax = plt.gca()
ax.axis([0, 6, 0, 10]) # Set x and y axis limits
```

## Scatter Plots
Demonstrates how to create scatter plots, including customizing point size, color, and adding labels and legends.

```python
import numpy as np

x = np.array([1, 2, 3, 4, 5, 6, 7, 8, 9, 10])
y = np.array([1, 2, 3, 4, 5, 6, 7, 8, 9, 10])

plt.figure()
plt.scatter(x, y, color='red', s=100) # Basic scatter plot

# Scatter plot with varying colors and labels
color_sequence = ["blue", "red", "green"]
colors = [color_sequence[i % len(color_sequence)] for i in range(len(x))]

plt.figure()
plt.scatter(x, y, c=colors, s=80)
plt.xlabel("X-axis")
plt.ylabel("Y-axis")
plt.show()

# Scatter plot with legend for different groups
plt.figure()
plt.xlabel('the number of times children kicked a ball')
plt.ylabel('the grade of the student')
plt.title('relationship between ball kicking and grades')
plt.scatter(x[:2], y[:2], s=100, c='brown', label='Tall students')
plt.scatter(x[2:], y[2:], s=100, c='orange', label='Short students')
plt.legend()
plt.show()
```

## Line Plots
Shows how to create line plots, useful for visualizing trends over a continuous range.

```python
l = np.array([1, 2, 3, 4, 5, 6, 7, 8, 9, 10])
e = l**2

plt.figure()
plt.plot(l, '-o', e, '-o') # Plotting multiple lines on the same graph
plt.show()
```

## Histograms
Illustrates how to create histograms to visualize the distribution of a dataset.

```python
population_ages = [22, 55, 62, 45, 21, 22, 34, 42, 42, 4, 99, 102, 110, 120, 121, 44, 43, 42]
bins = [0, 10, 20, 30, 40, 50, 60, 70, 80, 90, 100, 110, 120, 130]

plt.figure()
plt.hist(population_ages, bins, histtype='bar', rwidth=0.8)
plt.xlabel('x')
plt.ylabel('y')
plt.title('Interesting graph\ncheck it out')
plt.show()
```

## Bar Charts
Covers the creation of bar charts, which are effective for comparing categorical data.

```python
languages = np.array(['Python', 'SQL', 'Java', 'C++', 'JavaScript'])
pos = np.arange(len(languages))
popularity = [56, 39, 34, 34, 29]

plt.figure()
bars = plt.bar(pos, popularity, align='center', linewidth=5)
plt.xticks(pos, languages)
plt.ylabel('popularity')
plt.xlabel('languages')
plt.title('Popularity of Programming Language')
plt.show()
```

## Box Plots
Demonstrates how to create box plots (box-and-whisker plots) to show the distribution and central tendency of numerical data through their quartiles.

```python
np.random.seed(10)
data = np.random.normal(100, 10, 200) # Generate sample data

plt.figure()
plt.boxplot(data)
plt.show()

# Multiple box plots
value1 = [82, 76, 24, 40, 67, 75, 78, 71, 32, 98, 89, 82, 87, 66, 56, 52]
value2 = [62, 34, 45, 76, 87, 92, 65, 23.32, 97, 95, 31, 14, 71, 81, 18, 67]
value3 = [98, 56, 76, 54, 34, 25, 15, 47, 83, 47, 92, 43, 32, 98, 65, 12, 13, 30, 78]
value4 = [67, 98, 24, 73, 45, 60, 87, 14, 56, 69, 23, 97, 27, 18, 45, 30, 20, 80, 45]

box_plot_data = [value1, value2, value3, value4]

plt.figure()
plt.boxplot(box_plot_data)
plt.show()
```

## Pandas Integration
Shows how to integrate `pandas` DataFrames with `matplotlib` for data analysis and visualization, including reading CSV files, filtering data, and plotting directly from DataFrames.

```python
import pandas as pd

# Load data from CSV (assuming 'life.csv' is in '/content/drive/MyDrive/Untitled folder/')
df = pd.read_csv('/content/drive/MyDrive/Untitled folder/life.csv')
display(df.head(5)) # Display first 5 rows

# Box plot by category from DataFrame
df.boxplot(column='lifeExp', by='continent', grid=False)
plt.show()

# Scatter plot for specific country's GDP per capita over years
df[df['country'] == 'Afghanistan'].plot(kind='scatter', x='year', y='gdpPercap', color='brown')
plt.show()

# Life expectancy difference between years
df_2002 = df[df["year"] == 2002][["country", "lifeExp"]].rename(columns={"lifeExp": "lifeExp_2002"})
df_2007 = df[df["year"] == 2007][["country", "lifeExp"]].rename(columns={"lifeExp": "lifeExp_2007"})

df_diff = pd.merge(df_2002, df_2007, on="country")
df_diff["lifeExp_diff"] = df_diff["lifeExp_2007"] - df_diff["lifeExp_2002"]

plt.figure(figsize=(30, 10))
plt.xticks(rotation=90)
plt.scatter(df_diff["country"], df_diff["lifeExp_diff"], color="black", s=20)
plt.title("Life Expectancy Difference (2007 vs 2002)")
plt.ylabel("Life Expectancy Difference")
plt.xlabel("Country")
plt.show()
```

## Data Source
The notebook uses a dataset named `life.csv`, which is expected to be mounted from Google Drive at `/content/drive/MyDrive/Untitled folder/life.csv`. This dataset likely contains information related to countries, years, population, continents, life expectancy, and GDP per capita.
