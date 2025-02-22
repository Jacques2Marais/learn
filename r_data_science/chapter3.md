# Chapter 3: Data Visualization with `ggplot2`

Welcome to the exciting world of data visualization in R! In this chapter, we'll introduce you to `ggplot2`, a powerful and elegant package for creating graphics based on "The Grammar of Graphics".  `ggplot2` is a cornerstone of data science in R, known for its flexibility and ability to produce publication-quality visuals.

## Introduction to `ggplot2` Grammar of Graphics

`ggplot2` is based on the Grammar of Graphics, a conceptual framework that breaks down plots into distinct components. Understanding this grammar will empower you to create a wide range of visualizations and customize them effectively.

The fundamental components of a `ggplot2` plot are:

*   **Data:** The dataset you want to visualize (usually a data frame).
*   **Geometries (geoms):**  The visual marks that represent data points. Examples include points (for scatter plots), lines, bars, histograms, boxes, etc.
*   **Aesthetics (aes):**  Mappings that link variables in your data to visual properties of the geoms.  Common aesthetics include:
    *   `x`:  Position on the x-axis.
    *   `y`:  Position on the y-axis.
    *   `color`:  Color of the geom.
    *   `fill`:  Fill color of the geom (for areas like bars or polygons).
    *   `size`:  Size of the geom.
    *   `shape`:  Shape of points.
    *   `alpha`:  Transparency.
*   **Scales:** Control the mapping from data values to aesthetic values. For example, scales determine how numeric values are mapped to positions on axes, or how categories are mapped to colors. `ggplot2` automatically handles scales in many cases, but you can customize them.
*   **Coordinate system:**  Defines the 2D space in which your plot is drawn. The default is Cartesian coordinates, but others exist (e.g., polar coordinates).
*   **Facets:**  For creating subplots based on categorical variables, allowing you to visualize data across different groups.
*   **Themes:** Control the overall look and feel of your plot (e.g., background color, grid lines, font styles).

Building a `ggplot2` plot involves specifying these components layer by layer.

## Creating Basic Plots

Let's start with creating some fundamental plot types using `ggplot2`.  First, make sure you have `ggplot2` installed and loaded:

```R
# Install ggplot2 if needed
# install.packages("ggplot2")

library(ggplot2)
```

We'll use a built-in R dataset called `iris` for these examples.  `iris` contains measurements of sepal and petal length and width for three species of iris flowers.

```R
head(iris) # Take a look at the iris dataset
```

### Scatter Plots

Scatter plots are used to visualize the relationship between two numeric variables.

```R
ggplot(iris, aes(x = Sepal.Length, y = Sepal.Width)) + # Data and aesthetics
  geom_point() # Add points as geometries
```

**Explanation:**

1.  `ggplot(iris, aes(x = Sepal.Length, y = Sepal.Width))`:  This sets up the base plot.
    *   `ggplot(iris, ...)`:  Specifies that we're using the `iris` data frame.
    *   `aes(x = Sepal.Length, y = Sepal.Width)`:  Defines the aesthetics. We're mapping `Sepal.Length` to the x-axis and `Sepal.Width` to the y-axis.
2.  `geom_point()`:  Adds the "point" geometry layer. This tells `ggplot2` to represent each data point as a point on the plot.

**Adding more aesthetics:** Let's color the points by `Species`.

```R
ggplot(iris, aes(x = Sepal.Length, y = Sepal.Width, color = Species)) +
  geom_point()
```

Now, points are colored differently based on the `Species` variable. `ggplot2` automatically chooses distinct colors and creates a legend.

You can also control other aesthetics like `size` and `shape`:

```R
ggplot(iris, aes(x = Sepal.Length, y = Sepal.Width, color = Species, size = Petal.Length, shape = Species)) +
  geom_point(alpha = 0.7) # Adjust transparency with alpha
```

### Histograms

Histograms visualize the distribution of a single numeric variable.

```R
ggplot(iris, aes(x = Sepal.Length)) +
  geom_histogram() # Add histogram geometry
```

**Customizing histograms:**

*   `bins`: Control the number of bins (bars).
*   `fill`:  Set the fill color of the bars.
*   `color`: Set the outline color of the bars.

```R
ggplot(iris, aes(x = Sepal.Length)) +
  geom_histogram(bins = 20, fill = "skyblue", color = "black")
```

**Adding density curves:** You can overlay a density curve to visualize the probability density.

```R
ggplot(iris, aes(x = Sepal.Length)) +
  geom_histogram(aes(y = ..density..), bins = 20, fill = "skyblue", color = "black") + # Map density to y-axis
  geom_density(color = "red", size = 1.2) # Add density curve
```

### Bar Charts

Bar charts are used to display the counts or values of categorical variables.

Let's create a simple data frame for demonstration:

```R
fruit_sales <- data.frame(
  fruit = c("Apples", "Bananas", "Oranges", "Grapes"),
  sales = c(150, 200, 120, 180)
)
fruit_sales
```

Create a bar chart of fruit sales:

```R
ggplot(fruit_sales, aes(x = fruit, y = sales)) +
  geom_bar(stat = "identity", fill = "lightgreen", color = "black") # stat = "identity" for pre-calculated values
```

**Explanation:**

*   `geom_bar(stat = "identity", ...)`:  We use `stat = "identity"` because the `sales` values are already calculated in our `fruit_sales` data frame. If you just had counts of categories, you could use `stat = "count"` (the default for `geom_bar()`).

**Customizing bar charts:**

*   `fill`: Bar fill color.
*   `color`: Bar outline color.

## Customizing Plots for Clarity and Aesthetics

`ggplot2` offers extensive options for customizing plots to make them clear, informative, and visually appealing.

### Adding Titles and Labels

Use `labs()` to add titles and axis labels:

```R
ggplot(iris, aes(x = Sepal.Length, y = Sepal.Width, color = Species)) +
  geom_point() +
  labs(
    title = "Sepal Length vs. Sepal Width for Iris Species",
    x = "Sepal Length (cm)",
    y = "Sepal Width (cm)",
    color = "Iris Species" # Label for the color legend
  )
```

### Themes

Themes control the overall visual style of your plot. `ggplot2` comes with several built-in themes, and you can also create custom themes.

*   **Built-in themes:**  Examples include `theme_gray()`, `theme_bw()`, `theme_light()`, `theme_dark()`, `theme_minimal()`, `theme_void()`.

    ```R
    ggplot(iris, aes(x = Sepal.Length, y = Sepal.Width, color = Species)) +
      geom_point() +
      theme_bw() # Black and white theme
    ```

    Try different themes to see how they change the plot's appearance.

*   **Customizing themes:**  Use `theme()` to modify specific theme elements.

    ```R
    ggplot(iris, aes(x = Sepal.Length, y = Sepal.Width, color = Species)) +
      geom_point() +
      theme_minimal() + # Start with a minimal theme
      theme(
        plot.title = element_text(hjust = 0.5, size = 16, face = "bold"), # Center title, style it
        axis.title = element_text(size = 14),
        legend.position = "top" # Move legend to the top
      ) +
      labs(title = "Customized Scatter Plot")
    ```

### Scales

Scales control how data values are mapped to aesthetics. You can customize scales to:

*   Change axis limits and breaks.
*   Modify legend appearance.
*   Use different color palettes.
*   Format axis labels.

**Example: Customizing scales:**

```R
ggplot(iris, aes(x = Sepal.Length, y = Sepal.Width, color = Species)) +
  geom_point() +
  scale_x_continuous(limits = c(4, 8), breaks = seq(4, 8, by = 1)) + # Set x-axis limits and breaks
  scale_y_continuous(limits = c(2, 4.5)) + # Set y-axis limits
  scale_color_manual(values = c("setosa" = "blue", "versicolor" = "green", "virginica" = "purple"), # Custom colors
                       name = "Flower Type") + # Legend title
  labs(title = "Scatter Plot with Customized Scales")
```

*   `scale_x_continuous()`, `scale_y_continuous()`: For continuous x and y axes.  `limits` sets axis range, `breaks` specifies where tick marks should appear.
*   `scale_color_manual()`: For customizing colors when the `color` aesthetic is used. `values` sets the colors for each category, `name` sets the legend title.

### Faceting

Faceting creates subplots based on categorical variables. Use `facet_wrap()` or `facet_grid()`.

*   **`facet_wrap()`:** Creates a "wrapped" layout of subplots.

    ```R
    ggplot(iris, aes(x = Sepal.Length, y = Sepal.Width, color = Species)) +
      geom_point() +
      facet_wrap(~ Species) # Facet by Species
    ```

*   **`facet_grid()`:** Creates a grid layout, useful for faceting by two variables (rows and columns).

    ```R
    # Example with a hypothetical 'Region' variable in iris data (not actually present)
    iris$Region <- rep(c("Region A", "Region B"), each = 75) # Create a dummy Region variable

    ggplot(iris, aes(x = Sepal.Length, y = Sepal.Width, color = Species)) +
      geom_point() +
      facet_grid(Region ~ Species) # Facet by Region (rows) and Species (columns)
    ```

## Saving Plots

To save your `ggplot2` plots to files, use `ggsave()`.

```R
# Save the last created plot as "scatterplot.png" in your working directory
ggsave("scatterplot.png", width = 8, height = 6, units = "in") # Specify dimensions and units

# Save a specific plot object
my_plot <- ggplot(iris, aes(x = Sepal.Length, y = Sepal.Width)) + geom_point()
ggsave("my_scatterplot.pdf", plot = my_plot, width = 10, height = 8) # Save as PDF
```

`ggsave()` automatically detects the file type from the extension (`.png`, `.pdf`, `.jpg`, `.tiff`, etc.).

## Let's Practice!

1.  **Choose a dataset:**  Use the `iris` dataset or another dataset you've imported in Chapter 2.
2.  **Create scatter plots:**
    *   Explore relationships between different pairs of numeric variables using scatter plots.
    *   Experiment with coloring points by categorical variables.
    *   Adjust point size, shape, and transparency.
3.  **Create histograms:**
    *   Visualize the distribution of different numeric variables using histograms.
    *   Change the number of bins, fill color, and outline color.
    *   Overlay density curves.
4.  **Create bar charts:**
    *   If your dataset has categorical variables with counts or values, create bar charts.
    *   Customize bar colors.
5.  **Customize your plots:**
    *   Add titles and axis labels using `labs()`.
    *   Try different built-in themes.
    *   Experiment with customizing theme elements using `theme()`.
    *   Adjust axis limits and breaks using scales.
    *   If applicable, try faceting your plots using `facet_wrap()`.
6.  **Save your favorite plots** using `ggsave()`.

## Chapter Summary

In this chapter, you've unlocked the power of `ggplot2` for data visualization in R. You've learned:

*   The fundamental **Grammar of Graphics** concepts behind `ggplot2`.
*   How to create basic plots: **scatter plots**, **histograms**, and **bar charts**.
*   How to customize plots with **titles, labels, themes, and scales**.
*   Using **faceting** to create subplots for categorical comparisons.
*   How to **save plots** to files using `ggsave()`.

With `ggplot2` in your toolkit, you can now transform raw data into insightful and visually appealing graphics. In the next chapter, we'll move on to statistical analysis in R!
