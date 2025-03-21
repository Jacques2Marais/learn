# Chapter 7: Data Visualization with Matplotlib and Seaborn

Data visualization is a critical part of data analysis and communication. It allows you to explore patterns, trends, and insights in your data visually, and to effectively communicate your findings to others. Python offers excellent libraries for creating various types of plots and charts. In this chapter, we'll introduce two fundamental libraries: Matplotlib and Seaborn.

## Introduction to Matplotlib: Plots, Subplots, Customization

Matplotlib is the foundational plotting library in Python. It provides a wide range of 2D plotting capabilities and serves as the basis for many higher-level visualization libraries like Seaborn.

**Basic Plotting with Matplotlib:**

The `matplotlib.pyplot` module provides a convenient interface for creating plots.

**1. Line plots:**

Line plots are used to display the relationship between two continuous variables, often showing trends over time or ordered sequences.

```python
# Code cell
import matplotlib.pyplot as plt

x_values = [1, 2, 3, 4, 5]
y_values = [2, 4, 1, 3, 5]

plt.plot(x_values, y_values) # Create a line plot
plt.xlabel("X-axis") # Add x-axis label
plt.ylabel("Y-axis") # Add y-axis label
plt.title("Simple Line Plot") # Add plot title
plt.show() # Display the plot
```

**Customizing Line Plots:**

You can customize various aspects of line plots, such as line style, color, markers, and labels.

```python
# Code cell
import matplotlib.pyplot as plt

x = [1, 2, 3, 4, 5]
y1 = [2, 4, 1, 3, 5]
y2 = [3, 5, 2, 4, 6]

plt.plot(x, y1, label='Line 1', color='blue', linestyle='-', marker='o') # Customize line 1
plt.plot(x, y2, label='Line 2', color='red', linestyle='--', marker='s') # Customize line 2

plt.xlabel("X-axis")
plt.ylabel("Y-axis")
plt.title("Customized Line Plot")
plt.legend() # Show legend (labels for each line)
plt.grid(True) # Add grid lines
plt.xlim(0, 6) # Set x-axis limits
plt.ylim(0, 7) # Set y-axis limits
plt.show()
```

**2. Scatter plots:**

Scatter plots are used to display the relationship between two variables as points in a 2D plane. They are useful for visualizing correlations and distributions.

```python
# Code cell
import matplotlib.pyplot as plt

x = [1, 2, 3, 4, 5]
y = [2, 4, 1, 3, 5]

plt.scatter(x, y, color='green', marker='^', s=100) # Create a scatter plot
plt.xlabel("X-values")
plt.ylabel("Y-values")
plt.title("Scatter Plot")
plt.show()
```

**3. Bar plots:**

Bar plots are used to compare categorical data, showing the values of different categories as bars.

```python
# Code cell
import matplotlib.pyplot as plt

categories = ['A', 'B', 'C', 'D']
values = [25, 40, 30, 50]

plt.bar(categories, values, color=['skyblue', 'lightcoral', 'lightgreen', 'lightsalmon']) # Create a bar plot
plt.xlabel("Categories")
plt.ylabel("Values")
plt.title("Bar Plot")
plt.show()

# Horizontal bar plot
plt.barh(categories, values, color=['skyblue', 'lightcoral', 'lightgreen', 'lightsalmon']) # Create a horizontal bar plot
plt.xlabel("Values")
plt.ylabel("Categories")
plt.title("Horizontal Bar Plot")
plt.show()
```

**4. Histograms:**

Histograms are used to visualize the distribution of a single continuous variable, showing the frequency of values falling into different bins (intervals).

```python
# Code cell
import matplotlib.pyplot as plt
import numpy as np

data = np.random.randn(1000) # Generate 1000 random numbers from standard normal distribution

plt.hist(data, bins=30, color='gold', edgecolor='black') # Create a histogram with 30 bins
plt.xlabel("Values")
plt.ylabel("Frequency")
plt.title("Histogram")
plt.show()
```

**Subplots:**

You can create multiple plots within a single figure using subplots. `plt.subplot(rows, cols, plot_number)` creates a subplot in a grid of `rows` x `cols`, and `plot_number` specifies the position of the current subplot (starting from 1, row-major order).

```python
# Code cell
import matplotlib.pyplot as plt
import numpy as np

x = np.linspace(0, 10, 100)
y1 = np.sin(x)
y2 = np.cos(x)

plt.figure(figsize=(10, 5)) # Create a figure (optional, to set figure size)

plt.subplot(1, 2, 1) # 1 row, 2 columns, first subplot
plt.plot(x, y1, color='blue')
plt.title("Sine Wave")

plt.subplot(1, 2, 2) # 1 row, 2 columns, second subplot
plt.plot(x, y2, color='red')
plt.title("Cosine Wave")

plt.tight_layout() # Adjust subplot parameters for tight layout
plt.show()
```

## Introduction to Seaborn: Statistical Data Visualization

Seaborn is a higher-level visualization library built on top of Matplotlib. It provides a more convenient and aesthetically pleasing way to create statistical graphics. Seaborn is particularly well-suited for visualizing relationships between multiple variables in datasets.

**Common Seaborn Plot Types:**

**1. Scatter plots with `sns.scatterplot()`:** Enhanced scatter plots with options for color-coding and sizing points by additional variables.

```python
# Code cell
import seaborn as sns
import matplotlib.pyplot as plt
import pandas as pd

data = {
    'x_values': [1, 2, 3, 4, 5, 1, 2, 3, 4, 5],
    'y_values': [2, 4, 1, 3, 5, 3, 5, 2, 4, 6],
    'category': ['A', 'A', 'A', 'A', 'A', 'B', 'B', 'B', 'B', 'B']
}
df_scatter = pd.DataFrame(data)

sns.scatterplot(x='x_values', y='y_values', hue='category', style='category', size='y_values', data=df_scatter, sizes=(20, 200)) # Enhanced scatter plot
plt.title("Seaborn Scatter Plot")
plt.show()
```

**2. Histograms with `sns.histplot()` and distributions with `sns.displot()`:** More flexible histograms and distribution plots, including kernel density estimation (KDE).

```python
# Code cell
import seaborn as sns
import matplotlib.pyplot as plt
import numpy as np

data = np.random.randn(1000)

sns.histplot(data, bins=30, kde=True, color='skyblue') # Histogram with KDE
plt.title("Seaborn Histogram with KDE")
plt.xlabel("Values")
plt.ylabel("Frequency")
plt.show()

sns.displot(data, kind='hist', bins=30, kde=True, color='lightgreen') # Alternative way to create histogram with displot
plt.title("Seaborn displot (histogram)")
plt.show()

sns.displot(data, kind='kde', color='salmon') # Kernel Density Estimate plot
plt.title("Seaborn displot (KDE)")
plt.show()
```

**3. Box plots with `sns.boxplot()`:** Box plots visualize the distribution of a variable and detect outliers, comparing distributions across categories.

```python
# Code cell
import seaborn as sns
import matplotlib.pyplot as plt
import pandas as pd

data_box = {
    'category': ['A'] * 50 + ['B'] * 50,
    'values': np.concatenate([np.random.normal(25, 5, 50), np.random.normal(35, 8, 50)])
}
df_boxplot = pd.DataFrame(data_box)

sns.boxplot(x='category', y='values', data=df_boxplot, color='lightcoral') # Box plot
plt.title("Seaborn Box Plot")
plt.show()
```

**4. Violin plots with `sns.violinplot()`:** Similar to box plots but show the probability density of the data at different values, combining box plot elements with KDE.

```python
# Code cell
import seaborn as sns
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np

data_violin = {
    'category': ['X'] * 50 + ['Y'] * 50,
    'values': np.concatenate([np.random.normal(30, 7, 50), np.random.normal(40, 10, 50)])
}
df_violinplot = pd.DataFrame(data_violin)

sns.violinplot(x='category', y='values', data=df_violinplot, color='lightskyblue') # Violin plot
plt.title("Seaborn Violin Plot")
plt.show()
```

**5. Bar plots with `sns.barplot()`:** Seaborn bar plots are designed for statistical comparisons, often showing means and confidence intervals.

```python
# Code cell
import seaborn as sns
import matplotlib.pyplot as plt
import pandas as pd

data_barplot = {
    'category': ['Group 1', 'Group 2', 'Group 3'],
    'mean_values': [35, 42, 38],
    'std_dev': [3, 5, 4]
}
df_barplot = pd.DataFrame(data_barplot)

sns.barplot(x='category', y='mean_values', yerr='std_dev', data=df_barplot, color='lightgreen') # Bar plot with error bars
plt.xlabel("Groups")
plt.ylabel("Mean Values")
plt.title("Seaborn Bar Plot with Error Bars")
plt.show()
```

**6. Heatmaps with `sns.heatmap()`:** Heatmaps visualize 2D data (like matrices or correlation matrices) using color gradients to represent values.

```python
# Code cell
import seaborn as sns
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd

correlation_matrix = np.corrcoef(np.random.randn(10, 5).T) # Example correlation matrix (5x5)
df_heatmap = pd.DataFrame(correlation_matrix, columns=[f'Var{i+1}' for i in range(5)], index=[f'Var{i+1}' for i in range(5)])

sns.heatmap(df_heatmap, annot=True, cmap='coolwarm', fmt=".2f") # Heatmap with annotations, colormap, formatting
plt.title("Seaborn Heatmap (Correlation Matrix)")
plt.show()
```

**Customizing Seaborn Plots:**

Seaborn plots can be further customized using Matplotlib functions for titles, labels, legends, and more. Seaborn also provides themes and styles to control the overall appearance of plots.

```python
# Code cell
import seaborn as sns
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np

data_custom_style = {
    'categories': ['Cat A', 'Cat B', 'Cat C', 'Cat D'],
    'values': [30, 45, 25, 55]
}
df_custom_barplot = pd.DataFrame(data_custom_style)

sns.set_theme(style="darkgrid") # Set Seaborn theme
sns.barplot(x='categories', y='values', data=df_custom_barplot, palette="viridis") # Use a color palette
plt.title("Seaborn Bar Plot with Custom Theme and Palette", fontsize=14, fontweight='bold') # Customize title
plt.xlabel("Categories", fontsize=12) # Customize x-axis label
plt.ylabel("Values", fontsize=12) # Customize y-axis label
plt.xticks(rotation=45) # Rotate x-axis tick labels
plt.tight_layout()
plt.show()
```

Data visualization is an iterative process. You'll often create multiple plots, experiment with different types and customizations, and refine your visualizations to effectively explore and communicate your data insights. Matplotlib and Seaborn provide a rich set of tools to support this process.

**In this chapter, we've covered:**

*   Introduction to data visualization and its importance.
*   Basic plotting with Matplotlib: `plot()`, `scatter()`, `bar()`, `hist()`.
*   Customizing Matplotlib plots: labels, titles, legends, styles.
*   Subplots for creating multiple plots in one figure.
*   Introduction to Seaborn for statistical data visualization.
*   Common Seaborn plot types: `scatterplot()`, `histplot()`/`displot()`, `boxplot()`, `violinplot()`, `barplot()`, `heatmap()`.
*   Customizing Seaborn plots and using themes.

In the next chapter, we'll delve into statistical analysis with SciPy, exploring hypothesis testing, regression, and optimization techniques.
