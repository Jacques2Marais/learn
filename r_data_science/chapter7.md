# Chapter 7: Advanced Data Visualization

Welcome back to Advanced Data Visualization with R! In Chapter 3, you mastered the fundamentals of `ggplot2`. Now, we'll expand your visualization skills to create more dynamic and specialized plots. This chapter will cover interactive plots with `plotly`, geospatial data visualization with `leaflet`, and an introduction to building dashboards with `Shiny`.

## Creating Interactive Plots with `plotly`

`plotly` is a powerful R package for creating interactive web-based plots. It extends `ggplot2` and allows you to add interactivity to your visualizations, such as tooltips, zooming, panning, and animations.

### Basic `plotly` Plots from `ggplot2`

The easiest way to create `plotly` plots is to convert your `ggplot2` plots to interactive versions using the `ggplotly()` function.

```R
# Install plotly if needed
# install.packages("plotly")

library(plotly)
library(ggplot2)

# Create a ggplot2 scatter plot
scatter_plot <- ggplot(iris, aes(x = Sepal.Length, y = Sepal.Width, color = Species)) +
  geom_point() +
  labs(title = "Iris Sepal Dimensions")

# Convert to plotly plot
plotly_scatter <- ggplotly(scatter_plot)
plotly_scatter # Display interactive plot
```

Now, when you run this code, you'll see an interactive scatter plot in your Viewer pane or browser. Hover over points to see tooltips with data, and use the toolbar at the top to zoom, pan, and perform other interactions.

### Customizing `plotly` Plots

You can further customize `plotly` plots directly.

*   **Tooltips:** Control what information is displayed in tooltips using the `tooltip` argument in `aes()`.

    ```R
    ggplot(iris, aes(x = Sepal.Length, y = Sepal.Width, color = Species,
                     text = paste("Species:", Species, "<br>", # Custom tooltip text
                                  "Sepal Length:", Sepal.Length, "<br>",
                                  "Sepal Width:", Sepal.Width))) +
      geom_point() +
      labs(title = "Iris Sepal Dimensions with Custom Tooltips") +
      tooltip = "text" # Specify 'text' aesthetic for tooltip
    ```

*   **Markers and Hover Styles:** Customize marker appearance and hover effects using `marker` arguments in `geom_point()` and other geoms.

    ```R
    ggplot(iris, aes(x = Sepal.Length, y = Sepal.Width, color = Species)) +
      geom_point(size = 3, alpha = 0.8,
                 marker = list(symbol = 'circle', # Marker symbol
                               line = list(width = 1, color = 'black')), # Marker outline
                 hoverinfo = "text", # Show text tooltip on hover
                 text = ~paste("Species:", Species, "<br>Sepal Length:", Sepal.Length, "<br>Sepal Width:", Sepal.Width)) +
      labs(title = "Customized Scatter Plot with Hover Effects")
    ```

*   **Layout and Annotations:**  Customize plot layout, add annotations, shapes, and more using `layout()` function.

    ```R
    plot_with_annotations <- ggplotly(scatter_plot) %>%
      layout(
        title = list(text = "Interactive Iris Scatter Plot", x = 0.5), # Center title
        xaxis = list(title = "Sepal Length (cm)"),
        yaxis = list(title = "Sepal Width (cm)"),
        annotations = list(
          x = 5, y = 4,
          text = "Important Region",
          showarrow = TRUE,
          arrowhead = 4
        )
      )
    plot_with_annotations
    ```

*   **Interactive Widgets:** `plotly` can be integrated with `Shiny` to create interactive dashboards with widgets like sliders, dropdowns, etc., to control plot elements dynamically. We'll touch on `Shiny` later in this chapter.

## Geospatial Data Visualization with `leaflet`

`leaflet` is a popular R package for creating interactive maps. It's based on the Leaflet JavaScript library and makes it easy to visualize geospatial data in R.

### Creating Basic `leaflet` Maps

```R
# Install leaflet if needed
# install.packages("leaflet")

library(leaflet)

# Create a basic map centered at a location
leaflet() %>%
  setView(lng = 0, lat = 0, zoom = 2) # Set initial view: longitude, latitude, zoom level
```

This creates a basic world map centered at longitude 0, latitude 0, with a zoom level of 2.

### Adding Markers and Popups

*   **Markers:** Add markers to the map to represent locations.

    ```R
    # Sample locations (replace with your data)
    locations <- data.frame(
      city = c("London", "New York", "Tokyo"),
      lat = c(51.5, 40.7, 35.7),
      lng = c(-0.1, -74.0, 139.7)
    )

    leaflet() %>%
      setView(lng = 0, lat = 0, zoom = 2) %>%
      addMarkers(data = locations, ~lng, ~lat, popup = ~city) # Add markers from 'locations' data frame
    ```

*   **Popups:** Add popups that appear when you click on markers, displaying information.

    ```R
    leaflet() %>%
      setView(lng = 0, lat = 0, zoom = 2) %>%
      addMarkers(data = locations, ~lng, ~lat,
                 popup = ~paste("<b>City:</b>", city, "<br>", # HTML formatting in popup
                                "<b>Latitude:</b>", lat, "<br>",
                                "<b>Longitude:</b>", lng))
    ```

### Adding Layers and Tiles

*   **Tile Layers:**  Control the map's background tiles (map styles). `leaflet` provides various tile providers.

    ```R
    leaflet() %>%
      setView(lng = 0, lat = 0, zoom = 2) %>%
      addTiles() # Default OpenStreetMap tiles

    # Use different tile provider (e.g., Stamen Toner)
    leaflet() %>%
      setView(lng = 0, lat = 0, zoom = 2) %>%
      addProviderTiles(providers$Stamen.Toner)
    ```

    Explore `providers` list in `leaflet` documentation for many tile options.

*   **Adding Multiple Layers:** You can add multiple layers to a map (e.g., markers, polygons, lines, tile layers).

    ```R
    # Example with markers and different tile layer
    leaflet() %>%
      setView(lng = 0, lat = 0, zoom = 2) %>%
      addProviderTiles(providers$Esri.WorldStreetMap) %>% # Different tile layer
      addMarkers(data = locations, ~lng, ~lat, popup = ~city) # Markers layer
    ```

### Visualizing Geospatial Data

You can visualize geospatial data using various `leaflet` functions:

*   **`addPolygons()`:**  For drawing polygons (e.g., country boundaries, regions).
*   **`addCircles()`:** For drawing circles (e.g., to represent data points with size proportional to a value).
*   **`addPolylines()`:** For drawing lines (e.g., routes, paths).
*   **`addHeatmap()`:** For creating heatmaps of point densities.

**Example: Visualizing Earthquake Data (using sample data)**

```R
# Hypothetical earthquake data (replace with real data)
earthquakes <- data.frame(
  magnitude = sample(4:7, 100, replace = TRUE),
  lat = runif(100, -90, 90),
  lng = runif(100, -180, 180)
)

leaflet() %>%
  setView(lng = 0, lat = 0, zoom = 2) %>%
  addProviderTiles(providers$Stamen.TonerLite) %>%
  addCircles(data = earthquakes, ~lng, ~lat,
             radius = ~10^magnitude * 1000, # Radius scaled by magnitude
             weight = 1,
             color = "red",
             fillOpacity = 0.6,
             popup = ~paste("<b>Magnitude:</b>", magnitude))
```

## Creating Dashboards with `Shiny` (Introduction)

`Shiny` is a powerful R package for building interactive web applications and dashboards directly from R. It allows you to create web interfaces with plots, tables, widgets, and connect them to R code for dynamic and interactive data exploration.

### Basic `Shiny` App Structure

A basic `Shiny` app has two main components:

1.  **UI (User Interface):** Defines the layout and appearance of the app using functions like `fluidPage()`, `sidebarLayout()`, `mainPanel()`, `sidebarPanel()`, and input/output functions (e.g., `sliderInput()`, `plotOutput()`, `tableOutput()`).
2.  **Server:** Contains the R code that powers the app's logic, calculations, and plot generation. It reacts to user inputs and updates outputs accordingly.

**Example: Simple Shiny App**

Let's create a very basic Shiny app that displays a histogram of sepal lengths from the `iris` dataset, with a slider to control the number of bins.

**Create two files in your project directory:** `app.R` (or `server.R` and `ui.R`). For a simple app, `app.R` is often convenient.

**`app.R` content:**

```R
library(shiny)
library(ggplot2)

ui <- fluidPage( # Define UI
  titlePanel("Iris Sepal Length Histogram"), # App title
  sidebarLayout( # Layout with sidebar and main panel
    sidebarPanel( # Sidebar panel
      sliderInput("bins", # Input ID
                  "Number of bins:", # Slider label
                  min = 5, max = 50, value = 20) # Slider range and initial value
    ),
    mainPanel( # Main panel
      plotOutput("histPlot") # Output placeholder for plot (output ID)
    )
  )
)

server <- function(input, output) { # Define server logic
  output$histPlot <- renderPlot({ # Render plot output
    ggplot(iris, aes(x = Sepal.Length)) +
      geom_histogram(bins = input$bins, fill = "skyblue", color = "black") + # Bins from slider input
      labs(title = paste("Histogram with", input$bins, "bins"))
  })
}

shinyApp(ui = ui, server = server) # Run the Shiny app
```

**To run the app:**

1.  Save the `app.R` file.
2.  Open RStudio.
3.  Navigate to the directory containing `app.R`.
4.  Run the command `shiny::runApp("app.R")` in the R console. Or, if you have `app.R` open in the editor, click the "Run App" button in RStudio.

This will launch the Shiny app in your browser or Viewer pane. You'll see a histogram and a slider. Drag the slider to change the number of bins in the histogram dynamically.

### Key `Shiny` Components in the Example

*   **`ui <- fluidPage(...)`:**  Sets up the user interface using a fluid layout (adjusts to browser size).
*   **`titlePanel(...)`:**  App title.
*   **`sidebarLayout(...)`, `sidebarPanel(...)`, `mainPanel(...)`:**  Creates a layout with a sidebar and a main content area.
*   **`sliderInput("bins", ...)`:**  Creates a slider input widget. `"bins"` is the input ID, accessible in the server as `input$bins`.
*   **`plotOutput("histPlot")`:**  Creates a placeholder for a plot output. `"histPlot"` is the output ID, referenced in the server as `output$histPlot`.
*   **`server <- function(input, output) { ... }`:** Defines the server logic.
*   **`output$histPlot <- renderPlot({ ... })`:**  Renders a plot and assigns it to the `histPlot` output. `renderPlot()` is used for creating plots. The code inside `renderPlot({})` is reactive and will re-execute whenever inputs change.
*   **`input$bins`:**  Accesses the current value of the "bins" slider input in the server.
*   **`shinyApp(ui = ui, server = server)`:**  Runs the Shiny app, combining the UI and server definitions.

This is a very basic introduction to `Shiny`. `Shiny` is highly flexible and can be used to build complex interactive dashboards and web applications for data exploration, visualization, and more. We'll explore `Shiny` in more detail in later advanced chapters.

## Let's Practice!

1.  **`plotly` Exploration:**
    *   Take some `ggplot2` plots you created in Chapter 3 or 4. Convert them to interactive `plotly` plots using `ggplotly()`.
    *   Customize tooltips to display relevant information on hover.
    *   Experiment with marker styles and hover effects.
    *   Add annotations and customize the layout of your `plotly` plots.
2.  **`leaflet` Mapping:**
    *   Find or create a dataset with latitude and longitude information (e.g., locations of cities, points of interest, geographic events).
    *   Create a `leaflet` map and add markers for your locations.
    *   Customize marker popups to display information about each location.
    *   Try different tile layers to change the map style.
    *   If you have polygon or line data, experiment with `addPolygons()` or `addPolylines()`.
3.  **Basic `Shiny` App:**
    *   Create the simple histogram Shiny app example from this chapter (`app.R`). Run it and interact with the slider.
    *   Modify the app to create different types of plots (e.g., scatter plot, bar chart) and control different plot parameters with input widgets (e.g., dropdown for choosing variables, color pickers).

## Chapter Summary

In this chapter, you've expanded your data visualization capabilities to create advanced and interactive graphics in R. You've learned:

*   Creating **interactive plots with `plotly`** by converting `ggplot2` plots and customizing tooltips, markers, layout, and annotations.
*   **Geospatial data visualization with `leaflet`**, including creating basic maps, adding markers and popups, using different tile layers, and visualizing geospatial data with polygons, circles, and heatmaps.
*   An **introduction to building dashboards with `Shiny`**, understanding the basic structure of a Shiny app (UI and server), and creating a simple interactive histogram app with a slider input.

These advanced visualization techniques will enable you to create more engaging and informative data presentations, explore data interactively, and build powerful data applications. In the upcoming chapters, we'll continue to build on these skills and explore more advanced data science topics in R!
