# Chapter 13: Advanced Visualization Techniques

You've mastered basic visualizations and learned how to create interactive reports and dashboards. Now, let's explore **advanced visualization techniques** in Power BI to create even more compelling, insightful, and visually stunning data stories.

In this chapter, we'll delve into:

*   **Combo Charts (Combination Charts):** Combining different chart types in a single visual to show multiple data series effectively.
*   **Scatter Charts and Bubble Charts:** Visualizing relationships and distributions between numerical variables.
*   **Map Visualizations (Filled Maps, Shape Maps, ArcGIS Maps):**  Leveraging maps to visualize geographical data and spatial patterns.
*   **Treemap and Sunburst Charts:**  Displaying hierarchical data and part-to-whole relationships in a space-filling manner.
*   **Gauge and KPI Charts:**  Visualizing progress towards goals and key performance indicators.
*   **Funnel Charts and Waterfall Charts:**  Visualizing sequential processes and flow data.
*   **Custom Visuals:**  Extending Power BI's visualization library with custom visuals from the marketplace or by creating your own.

## 1. Combo Charts (Combination Charts)

**Combo charts** combine two or more chart types in a single visual, typically a column chart combined with a line chart. This is useful for:

*   **Showing Multiple Data Series with Different Scales:**  Displaying data series that have significantly different value ranges on the same chart without distorting the visual. For example, showing sales revenue (in millions) and order count (in thousands) together.
*   **Highlighting Relationships Between Different Metrics:**  Visually comparing trends and relationships between different types of data. For example, showing sales revenue and profit margin trends together over time.
*   **Enhancing Visual Storytelling:**  Creating more engaging and informative visuals by combining different chart types to emphasize specific insights.

**Types of Combo Charts in Power BI:**

*   **Clustered Column and Line Chart:**  Combines clustered columns (for categorical comparison) with a line chart (for trend visualization).
*   **Stacked Column and Line Chart:** Combines stacked columns (for showing parts of a whole within categories) with a line chart.
*   **Line and Stacked Column Chart:** (Less common) Line chart in front of stacked columns.

**Creating a Combo Chart:**

1.  **Select a Combo Chart Type:** In the "Visualizations" pane, choose either "Clustered column and line chart" or "Stacked column and line chart."
2.  **Add Data Fields:**
    *   **Shared Axis:** Drag a categorical or time-based field to the "Shared axis" field well (this will be the common axis for both chart types).
    *   **Column Values:** Drag one or more numeric fields to the "Column values" field well (these will be displayed as columns).
    *   **Line Values:** Drag one or more numeric fields to the "Line values" field well (these will be displayed as lines).
    *   **Column Series/Line Series (Optional):**  Use these field wells to add a categorical field to create separate series for columns or lines (e.g., different lines for different product categories).
    *   **Legend, Tooltips, etc.:**  Use other field wells as needed.
3.  **Format Your Combo Chart:**  Customize formatting options for columns, lines, axes, data labels, etc., in the "Format" pane. Pay attention to color contrast and clarity when combining different chart types.

**Example: Sales Revenue and Order Count Trend**

Create a combo chart showing monthly sales revenue (columns) and order count (line) over time. Use "Date"[Month-Year] as "Shared Axis," "Total Revenue" measure as "Column values," and "Order Count" measure as "Line values."

## 2. Scatter Charts and Bubble Charts

**Scatter charts** and **bubble charts** are used to visualize relationships and distributions between **numerical variables**.

*   **Scatter Chart:**
    *   **Purpose:**  Showing the relationship or correlation between two numerical variables.  Identifying clusters, outliers, and patterns in the distribution of data points.
    *   **Axes:**  X-axis and Y-axis both represent numerical variables.
    *   **Data Points:** Each data point represents a single observation, plotted based on its X and Y values.
    *   **Use Cases:**  Relationship between advertising spend and sales revenue, correlation between customer age and purchase amount, distribution of product prices and ratings.

*   **Bubble Chart:**
    *   **Extension of Scatter Chart:**  Similar to a scatter chart but adds a third numerical variable represented by the **size of the bubbles**.
    *   **Bubble Size:**  Bubble size encodes an additional dimension of data, allowing you to visualize three numerical variables simultaneously.
    *   **Use Cases:**  Sales revenue (Y-axis) vs. profit margin (X-axis), with bubble size representing market share; customer lifetime value (Y-axis) vs. customer acquisition cost (X-axis), with bubble size representing customer count.

**Creating Scatter Charts and Bubble Charts:**

1.  **Select Scatter Chart or Bubble Chart:** In the "Visualizations" pane, choose "Scatter chart" or "Bubble chart."
2.  **Add Data Fields:**
    *   **X Axis:** Drag a numerical field to the "X Axis" field well.
    *   **Y Axis:** Drag another numerical field to the "Y Axis" field well.
    *   **Details:** Drag a categorical field to the "Details" field well to create separate data points for each category (optional).
    *   **Size (for Bubble Chart):** For bubble charts, drag a third numerical field to the "Size" field well to control bubble size.
    *   **Legend, Tooltips, etc.:** Use other field wells as needed.
3.  **Format Your Chart:** Customize formatting options for axes, data points, colors, bubble sizes, data labels, etc., in the "Format" pane.

**Example: Sales vs. Profit Margin Bubble Chart**

Create a bubble chart showing "Profit Margin" (X-axis) vs. "Sales Revenue" (Y-axis) for different "Product Categories," with bubble size representing "Order Count."

## 3. Map Visualizations

Power BI offers powerful map visualizations for displaying **geographical data** and **spatial patterns**.

**Types of Map Visualizations in Power BI:**

*   **Map (Basic Map):**
    *   **Purpose:**  Displaying data points on a map based on location data (latitude/longitude or geographic names).
    *   **Location Types:**  Supports various location types: latitude/longitude, addresses, city names, country names, regions, etc. Power BI uses Bing Maps for geocoding.
    *   **Data Representation:**  Data points can be represented as bubbles (sized by a measure) or categories (colored by a category).
    *   **Use Cases:**  Sales by region, customer locations, store locations, geographic distribution of website traffic.

*   **Filled Map (Choropleth Map):**
    *   **Purpose:**  Displaying data aggregated by geographical areas (regions, countries, states).  Color-codes geographical areas based on a measure value.
    *   **Data Representation:**  Geographical areas are filled with colors based on a measure value, creating a heatmap-like effect. Color intensity represents the magnitude of the measure.
    *   **Use Cases:**  Sales by state, population density by country, average income by region, election results by county.

*   **Shape Map:**
    *   **Purpose:**  Similar to Filled Map but uses custom shapes instead of standard map regions.  Allows you to visualize data on non-standard geographical areas or custom regions (e.g., sales territories, building floor plans).
    *   **Custom Shapes:**  Requires custom shape files (TopoJSON format) to define the shapes.
    *   **Use Cases:**  Visualizing data on sales territories, organizational charts, building layouts, custom geographical regions not available in standard maps.

*   **ArcGIS Maps for Power BI (Integration with Esri ArcGIS):**
    *   **Advanced Mapping Capabilities:**  Leverages the powerful mapping platform of Esri ArcGIS.  Provides more advanced mapping features, basemaps, spatial analysis capabilities, and access to ArcGIS Online data.
    *   **Requires ArcGIS Subscription (for some features):**  Basic ArcGIS Maps functionality is available in Power BI, but advanced features and ArcGIS Online data access may require an Esri ArcGIS subscription.
    *   **Use Cases:**  Advanced spatial analysis, combining Power BI data with ArcGIS Online geospatial data, creating sophisticated interactive maps with rich basemaps and layers.

**Creating Map Visualizations:**

1.  **Select Map Visual Type:** In the "Visualizations" pane, choose "Map," "Filled Map," "Shape Map," or "ArcGIS Maps for Power BI."
2.  **Add Location Data:**
    *   **Location Field Well:** Drag a field containing location information (geographic names, addresses, latitude/longitude) to the "Location" field well.
    *   **Latitude and Longitude Field Wells (for Basic Map):**  Alternatively, for basic maps, you can drag latitude and longitude fields to the "Latitude" and "Longitude" field wells for more precise point placement.
3.  **Add Data Values (Measures):**
    *   **Size (for Basic Map and Bubble Size):** Drag a measure to the "Size" field well to size bubbles on the map based on the measure value.
    *   **Color Saturation (for Filled Map and Color Coding):** Drag a measure to the "Color saturation" field well to color-code map areas based on the measure value.
    *   **Category (for Color Coding):** Drag a categorical field to the "Legend" or "Category" field well to color-code data points or map areas by category.
    *   **Tooltips, etc.:** Use other field wells as needed.
4.  **Format Your Map:** Customize map styles, data colors, bubble sizes, map controls, labels, and other formatting options in the "Format" pane.

**Example: Sales by Region Filled Map**

Create a filled map showing "Total Sales" by "Region." Use "Region" field for "Location" and "Total Sales" measure for "Color saturation."

## 4. Treemap and Sunburst Charts

**Treemaps** and **sunburst charts** are excellent for visualizing **hierarchical data** and **part-to-whole relationships** in a space-filling manner.

*   **Treemap:**
    *   **Hierarchical Rectangles:** Displays hierarchical data as a set of nested rectangles.  The size of each rectangle represents the value of a measure for that category.  Hierarchical levels are represented by nested rectangles within larger rectangles.
    *   **Space-Filling:**  Efficiently uses space to display many categories and subcategories.
    *   **Use Cases:**  Sales by product category and subcategory, website traffic by source and sub-source, storage space usage by folder and subfolder.

*   **Sunburst Chart (Multi-level Pie Chart):**
    *   **Hierarchical Rings:** Displays hierarchical data as a series of concentric rings.  Each ring represents a level in the hierarchy.  Angles of segments represent proportions within each level.
    *   **Multi-Level Part-to-Whole:**  Shows how categories are broken down into subcategories and their proportions at each level.
    *   **Use Cases:**  Sales by region, country, and city; organizational hierarchy; file system structure.

**Creating Treemaps and Sunburst Charts:**

1.  **Select Treemap or Sunburst Chart:** In the "Visualizations" pane, choose "Treemap" or "Sunburst chart."
2.  **Add Hierarchical Categories:**
    *   **Category/Groups (for Treemap):** Drag one or more categorical fields (representing hierarchy levels) to the "Category" or "Group" field wells (depending on visual type).  Order matters for hierarchy levels.
    *   **Hierarchy (for Sunburst Chart):** Drag categorical fields in hierarchical order to the "Hierarchy" field well.
3.  **Add Data Values (Measures):**
    *   **Values:** Drag a measure to the "Values" field well to determine the size of rectangles (treemap) or segment angles (sunburst).
    *   **Details, Tooltips, etc.:** Use other field wells as needed.
4.  **Format Your Chart:** Customize colors, labels, data labels, and tooltips in the "Format" pane to enhance readability and visual appeal.

**Example: Product Category and Subcategory Treemap**

Create a treemap showing "Total Sales" by "Category" and "Subcategory." Use "Category" and "Subcategory" fields for "Category" field well (in that order), and "Total Sales" measure for "Values."

## 5. Gauge and KPI Charts

**Gauge charts** and **KPI (Key Performance Indicator) charts** are designed to visualize progress towards goals and track KPIs.

*   **Gauge Chart:**
    *   **Purpose:**  Visualizing progress towards a target or goal.  Showing a single metric value in relation to a target value and a maximum value.
    *   **Gauge Scale:**  Displays a radial gauge with a scale representing the range from minimum to maximum value.
    *   **Target Value:**  Indicates the target or goal value on the gauge scale.
    *   **Current Value:**  Shows the current metric value on the gauge scale, indicating progress towards the target.
    *   **Use Cases:**  Sales performance against target, website traffic towards a goal, project completion percentage.

*   **KPI Chart:**
    *   **Purpose:**  Quickly visualizing KPIs and their status.  Showing a metric value, a target value, and a status indicator (trend or variance).
    *   **Key Components:**
        *   **Value:**  The current KPI value.
        *   **Goal:**  The target or goal value for the KPI.
        *   **Status Indicator:**  Visual cue (trend arrow, color) indicating whether the KPI is on track, improving, or declining compared to the target or previous period.
        *   **Trend Axis (Optional):**  A small line chart showing the trend of the KPI over time.
    *   **Use Cases:**  Sales KPI dashboard, website traffic KPI monitoring, project status dashboard.

**Creating Gauge and KPI Charts:**

1.  **Select Gauge Chart or KPI Chart:** In the "Visualizations" pane, choose "Gauge" or "KPI."
2.  **Add Data Fields:**
    *   **Value (for Gauge and KPI):** Drag a measure to the "Value" field well (this is the current metric value).
    *   **Target value (for Gauge and KPI):** Drag a measure or a fixed value to the "Target value" or "Goal" field well (this is the target or goal value).
    *   **Minimum value and Maximum value (for Gauge):**  Optionally, specify minimum and maximum values for the gauge scale in the respective field wells. If not specified, Power BI auto-determines them.
    *   **Trend axis (for KPI):**  Optionally, drag a date or time-based field to the "Trend axis" field well to show a trend line in the KPI chart.
    *   **Indicator, Trend, Goal (for KPI):** (Alternative field wells for KPI chart, depending on visual version).
    *   **Category, Tooltips, etc.:** Use other field wells as needed.
3.  **Format Your Chart:** Customize gauge scales, colors, target markers, data labels, KPI indicators, and other formatting options in the "Format" pane.

**Example: Sales Performance Gauge Chart**

Create a gauge chart showing "Total Sales" as the "Value," and a fixed value (e.g., 1,000,000) as the "Target value," to visualize sales progress towards a million-dollar goal.

## 6. Funnel Charts and Waterfall Charts

**Funnel charts** and **waterfall charts** are specialized visuals for specific data types and analytical purposes.

*   **Funnel Chart:**
    *   **Purpose:**  Visualizing a sequential process or flow, showing stages and drop-off rates between stages.  Commonly used for sales funnels, conversion funnels, and pipeline analysis.
    *   **Funnel Shape:**  Displays data in a funnel shape, with each stage represented as a section of the funnel.  The width of each section is proportional to the value at that stage.
    *   **Sequential Stages:**  Stages are ordered sequentially, typically from largest to smallest value, representing a flow or progression.
    *   **Use Cases:**  Sales funnel analysis (leads, prospects, qualified leads, opportunities, closed deals), website conversion funnel (visits, product views, add to cart, checkout, completed purchase), application pipeline (applications, interviews, offers, hires).

*   **Waterfall Chart (Bridge Chart):**
    *   **Purpose:**  Showing the cumulative effect of sequential positive and negative values (changes) on an initial value.  Understanding the composition of a final value by breaking it down into contributing factors.
    *   **Floating Columns:**  Displays a series of floating columns that "bridge" from a starting value to an ending value.
    *   **Color-Coded Changes:**  Typically uses different colors to distinguish between positive increases (e.g., revenue increases) and negative decreases (e.g., expenses).
    *   **Use Cases:**  Profit and loss analysis (showing how revenue, cost of goods sold, operating expenses, etc., contribute to net profit), budget variance analysis, inventory flow analysis.

**Creating Funnel Charts and Waterfall Charts:**

1.  **Select Funnel Chart or Waterfall Chart:** In the "Visualizations" pane, choose "Funnel chart" or "Waterfall chart."
2.  **Add Data Fields:**
    *   **Category (for Funnel and Waterfall):** Drag a categorical field to the "Category" or "Axis" field well to define the stages or categories.  Order matters for funnel charts (stage sequence).
    *   **Values (for Funnel and Waterfall):** Drag a measure to the "Values" field well to represent the magnitude at each stage or the change value.
    *   **Breakdown (for Waterfall - Optional):**  Optionally, drag another categorical field to the "Breakdown" or "Legend" field well to further break down the waterfall columns into sub-categories.
    *   **Tooltips, etc.:** Use other field wells as needed.
3.  **Format Your Chart:** Customize colors, labels, data labels, column spacing, connector lines (waterfall), and other formatting options in the "Format" pane.

**Example: Sales Funnel Chart**

Create a funnel chart showing "Sales Stage" (e.g., Leads, Prospects, Qualified Leads, Opportunities, Closed) as "Category" and "Opportunity Count" as "Values" to visualize the sales conversion funnel.

## 7. Custom Visuals

Power BI's built-in visualization library is extensive, but you can further extend it with **custom visuals**.

*   **Power BI Visuals Marketplace:**  Microsoft and the Power BI community provide a marketplace of **custom visuals**.  These are visuals created by third-party developers that you can import into Power BI Desktop and use in your reports.
    *   **Get More Visuals:** In the "Visualizations" pane, click the ellipsis (...) and choose "Get more visuals." This opens the Power BI Visuals marketplace.
    *   **Browse and Import:**  Browse the marketplace, search for visuals by category or keyword, preview visuals, read descriptions and reviews, and import visuals directly into your Power BI Desktop.
*   **Types of Custom Visuals:**  The marketplace offers a wide range of custom visuals, including:
    *   **Advanced Charts:**  Specialized chart types not available in the standard library (e.g., network diagrams, Gantt charts, bullet charts, advanced time-series charts).
    *   **Industry-Specific Visuals:**  Visuals designed for specific industries or domains (e.g., financial charts, manufacturing process visuals, healthcare dashboards).
    *   **Visually Enhanced Visuals:**  Visuals with unique aesthetics, animations, or interactive features.
*   **Creating Your Own Custom Visuals (Advanced):**  If you have web development skills (HTML, CSS, JavaScript, TypeScript), you can even create your own custom visuals for Power BI using the Power BI visuals SDK. This is an advanced topic beyond the scope of this chapter.

**Using Custom Visuals:**

1.  **Import Custom Visual:**  Import custom visuals from the marketplace into your Power BI Desktop.  They will appear as new icons in your "Visualizations" pane.
2.  **Use Like Built-in Visuals:**  Use custom visuals just like built-in visuals. Select the custom visual type, and add data fields to its field wells.
3.  **Formatting and Properties:**  Custom visuals often have their own unique formatting options and properties, which you can customize in the "Format" pane.

**Caution with Custom Visuals:**

*   **Security and Trust:**  Be cautious when importing custom visuals from the marketplace, especially from unverified sources.  Ensure you trust the source and understand the visual's functionality.
*   **Performance:**  Some custom visuals might have performance implications, especially if they are complex or not well-optimized.  Test performance carefully.
*   **Support and Updates:**  Custom visuals are maintained by third-party developers.  Support and updates might vary.

## Practice Advanced Visualizations

Now it's your turn to practice creating advanced visualizations in Power BI Desktop!

1.  **Create Combo Charts:**  Build combo charts to visualize multiple data series with different scales or to highlight relationships between metrics.
2.  **Experiment with Scatter and Bubble Charts:**  Create scatter charts and bubble charts to explore relationships between numerical variables and identify data distributions.
3.  **Build Map Visualizations:**  Create map visualizations (filled maps, basic maps) to display geographical data and spatial patterns.
4.  **Design Treemaps and Sunburst Charts:**  Use treemaps and sunburst charts to visualize hierarchical data and part-to-whole relationships.
5.  **Create Gauge and KPI Charts:**  Build gauge and KPI charts to visualize progress towards goals and track key performance indicators.
6.  **Explore Funnel and Waterfall Charts:**  Use funnel charts to visualize sequential processes and waterfall charts to show cumulative effects of changes.
7.  **Browse and Import Custom Visuals:**  Explore the Power BI Visuals marketplace, import a few interesting custom visuals, and experiment with using them in your reports.

By practicing these advanced visualization techniques, you'll expand your Power BI visualization toolkit and be able to create even more impactful and insightful data stories! In the next chapter, we'll move on to **Custom Visuals and Themes**, where you'll learn how to further customize the look and feel of your Power BI reports to create visually stunning and branded BI solutions!
