# Chapter 12: Interactive Reports and Dashboards

Welcome to the exciting world of **Interactive Reports and Dashboards in Power BI!**  In the previous chapter, you learned how to create basic visualizations. Now, we'll take it a step further and learn how to combine these visuals into interactive reports and dashboards that empower users to explore data and gain deeper insights.

## What are Interactive Reports and Dashboards?

*   **Interactive Reports:**  Power BI reports are more than just static collections of charts. They are designed to be **interactive**, allowing users to explore data dynamically.  Users can:
    *   **Filter data:** Using slicers, visual filters, and cross-filtering.
    *   **Drill down:** Explore data at different levels of detail.
    *   **Highlight data:** Select data points to emphasize specific information.
    *   **Cross-highlight:** See how selections in one visual affect other visuals on the page.
    *   **Ask questions:** Use Q&A to query data in natural language.

*   **Dashboards:**  Power BI dashboards are **single-page summaries** of the most important information from one or more underlying reports and datasets.  Dashboards are designed for **at-a-glance monitoring** of key performance indicators (KPIs) and critical business metrics.  Key features of dashboards:
    *   **Single-Page View:**  Dashboards are always single-page, providing a consolidated overview.
    *   **Pinning Visuals:**  Visuals from reports are "pinned" to dashboards.  Dashboards are essentially collections of pinned visuals.
    *   **Data Refresh:** Dashboards reflect the latest data from the underlying datasets (based on refresh schedules).
    *   **Limited Interactivity (compared to Reports):**  Dashboards are primarily for viewing information, not deep data exploration.  Clicking on a visual in a dashboard typically navigates you back to the underlying report for more detailed analysis.
    *   **Designed for Monitoring:**  Dashboards are ideal for executives, managers, and anyone who needs a high-level overview of business performance.

**Key Elements of Interactive Reports and Dashboards:**

*   **Multiple Visuals:** Combining different types of visuals (charts, tables, cards, maps) on a single report page or dashboard to provide a comprehensive view of data.
*   **Slicers:**  Interactive filters that allow users to easily segment and filter data.
*   **Filters Pane:**  A pane in Power BI Desktop and Service that allows report authors and users to manage filters at the visual, page, and report levels.
*   **Visual Interactions (Cross-filtering and Cross-highlighting):**  Built-in interactivity that allows visuals to respond to selections in other visuals, creating a dynamic exploration experience.
*   **Drill-Down and Drill-Through:**  Features that allow users to navigate to more detailed levels of data within visuals or to related report pages.
*   **Bookmarks and Selection Pane:**  Features for saving and managing different report views and selections.
*   **Buttons and Navigation:**  Adding buttons and navigation elements to create guided report experiences.
*   **Themes and Formatting:**  Consistent visual design and formatting to enhance report aesthetics and professionalism.

## Building Interactive Reports

Let's explore how to build interactive reports in Power BI Desktop:

**1. Combine Multiple Visuals on a Report Page:**

*   **Add multiple visuals** to a report page by selecting different visual types from the "Visualizations" pane and positioning them on the canvas.
*   **Arrange visuals logically** to tell a data story and guide the user's eye.
*   **Consider visual hierarchy:**  Place the most important visuals prominently.
*   **Use white space effectively:**  Don't overcrowd the page.

**2. Add Slicers for Filtering:**

*   **Select the "Slicer" visual type** from the "Visualizations" pane.
*   **Drag a field** (typically a categorical or date field) to the "Field" well of the slicer.
*   **Format the slicer:**  Customize slicer type (list, dropdown, date range), appearance, and selection mode in the "Format" pane.
*   **Position slicers** strategically on the report page for easy access.

**3. Utilize the Filters Pane:**

*   **Filters Pane Location:**  The "Filters" pane is usually located on the right side of the Report View in Power BI Desktop and Service. If you don't see it, check the "View" ribbon and ensure "Filters pane" is checked.
*   **Filter Levels:** The Filters pane allows you to manage filters at three levels:
    *   **Visual-level filters:** Filters applied only to a specific selected visual.
    *   **Page-level filters:** Filters applied to all visuals on the current report page.
    *   **Report-level filters:** Filters applied to all pages in the entire report.
*   **Adding Filters:**
    *   **Drag fields** from the "Fields" pane to the "Filters on this visual," "Filters on this page," or "Filters on all pages" sections in the Filters pane.
    *   **Configure filter types and conditions:**  Choose filter types (basic filtering, advanced filtering, top N filtering) and set filter conditions (e.g., "is," "is not," "contains," "is greater than," date ranges).
*   **Filter Interactions:**  Understand how filters at different levels interact with each other and with slicers and visual interactions.

**4. Explore Visual Interactions (Cross-filtering and Cross-highlighting):**

*   **Default Interactions:** By default, visuals in Power BI are set to **cross-filter** each other.  When you select data points in one visual, other visuals on the page will automatically filter to show data related to your selection.
*   **Cross-highlighting:**  In addition to filtering, visuals can also **cross-highlight**. When you select data in one visual, related data points in other visuals are highlighted (emphasized), while non-related data points are dimmed.
*   **Customizing Visual Interactions:**  You can customize visual interactions to control how visuals affect each other:
    *   **Format Ribbon -> Edit Interactions:**  Select a visual, go to the "Format" ribbon, and click "Edit interactions."
    *   **Interaction Icons:**  Interaction icons will appear above all other visuals on the page.
    *   **Choose Interaction Type:** For each visual, you can choose:
        *   **Filter Icon (Funnel Icon):**  Cross-filtering (default).
        *   **Highlight Icon (Highlight Brush Icon):** Cross-highlighting.
        *   **None Icon (No Icon):**  No interaction.
    *   **Click Interaction Icons:** Click the interaction icons to change the interaction type between the selected visual and other visuals.

**5. Implement Drill-Down and Drill-Through:**

*   **Drill-Down:**  Allows users to explore data hierarchies within a visual.  For example, in a column chart showing sales by year, users can drill down to see sales by quarter within a selected year, then drill down further to months, and so on.
    *   **Enable Drill-Down:**  Ensure your visual has a hierarchy defined in its "Axis" field well (e.g., Year > Quarter > Month).
    *   **Drill-Down Controls:**  Use the drill-down controls in the visual header (drill-down icon, drill-up icon, expand all down one level icon) to navigate the hierarchy.
*   **Drill-Through:**  Allows users to navigate from a summary visual to a **separate report page** containing more detailed information related to the selected data point(s).
    *   **Create a Drill-Through Page:**  Create a new report page that will serve as your drill-through page.  This page should contain visuals that show detailed information related to the entity you want to drill through (e.g., order details, customer details).
    *   **Add Drill-Through Filters to Drill-Through Page:**  On the drill-through page, drag the field you want to drill through (e.g., "Product Category") to the "Drill-through filters" field well in the "Visualizations" pane (Filters on this page section).
    *   **Enable Drill-Through in Source Visual:**  In the visual from which you want to drill through (the source visual), right-click on a data point (e.g., a column in a column chart).  You should see a "Drill through" option in the context menu, listing the drill-through page you created.

**6. Utilize Bookmarks and Selection Pane (for Advanced Interactivity):**

*   **Bookmarks:**  Allow you to capture and save specific report views (including filters, slicer selections, visual states, drill-down levels).  Users can then easily switch between these saved views by clicking on bookmarks.
    *   **View Ribbon -> Bookmarks Pane:** Open the Bookmarks pane.
    *   **Create Bookmarks:**  Set up your report view as desired (apply filters, make selections, drill down). Click "Add" in the Bookmarks pane to create a bookmark capturing the current view.  Rename bookmarks for clarity.
    *   **Apply Bookmarks:**  Click on a bookmark in the Bookmarks pane to apply the saved view.
    *   **Link Bookmarks to Buttons/Images:**  You can link bookmarks to buttons or images to create navigation elements that trigger bookmark views.
*   **Selection Pane:**  Allows you to manage the layering and visibility of visuals and other report elements.
    *   **View Ribbon -> Selection Pane:** Open the Selection pane.
    *   **Visual Layers:** The Selection pane shows a list of all visuals and elements on the current page, in layers.  You can reorder layers, hide/show visuals (using the "eye" icon), and group visuals.
    *   **Combine with Bookmarks:**  Use the Selection pane in conjunction with bookmarks to create advanced interactive effects, such as showing/hiding groups of visuals based on bookmark selections.

## Creating Dashboards in Power BI Service

Dashboards are created and viewed in the **Power BI Service** (not in Power BI Desktop).

**Steps to Create a Dashboard:**

1.  **Publish Your Report to Power BI Service:**  First, you need to publish your Power BI Desktop report to the Power BI Service.  In Power BI Desktop, go to **Home Ribbon -> Publish**.  Choose your desired workspace in the Power BI Service to publish to.
2.  **Go to Power BI Service (Web Browser):**  Open a web browser and go to app.powerbi.com.  Sign in to your Power BI account.
3.  **Navigate to Your Report:**  In the Power BI Service, navigate to the workspace where you published your report.  Find your report in the "Reports" section.
4.  **Pin Visuals to a New Dashboard:**
    *   **Open your report** in the Power BI Service.
    *   **Hover over the visual** you want to add to a dashboard.  A "Pin visual" icon (thumbtack icon) will appear in the visual header.
    *   **Click "Pin visual."**
    *   **"Pin to dashboard" Dialog:**  The "Pin to dashboard" dialog will appear.
        *   **Choose "New dashboard"** to create a new dashboard.  Enter a name for your dashboard.
        *   **Choose "Existing dashboard"** to pin to an existing dashboard (if you have one).
    *   **Click "Pin."**
5.  **Repeat Pinning for Other Visuals:**  Repeat step 4 to pin other visuals from your report (or from other reports) to your dashboard.
6.  **View Your Dashboard:**  After pinning visuals, navigate to the "Dashboards" section in your workspace.  You should see your newly created dashboard.  Click on it to view your dashboard.
7.  **Arrange and Resize Tiles:**  In the dashboard view, you can:
    *   **Drag tiles** (pinned visuals) to rearrange their position on the dashboard.
    *   **Resize tiles** by dragging the handles on the corners of tiles.
    *   **Customize Dashboard Layout:**  Arrange tiles to create a visually appealing and informative dashboard layout.
8.  **Add Dashboard Tiles (Beyond Pinned Visuals):**  Dashboards can also include tiles beyond just pinned visuals:
    *   **Add Tile Button:**  In the dashboard view, click **"Edit" -> "+ Add tile"**.
    *   **Tile Types:**  You can add tiles for:
        *   **Web content:** Embed web pages, videos, etc.
        *   **Images:** Add images and logos.
        *   **Text boxes:** Add text headings, descriptions, and annotations.
        *   **Real-time data streaming tiles:** (Advanced) Connect to real-time data streams.

## Best Practices for Interactive Reports and Dashboards

*   **Design for Your Audience:**  Consider your target audience and their information needs when designing reports and dashboards.
*   **Focus on Key Metrics (Dashboards):** Dashboards should focus on the most critical KPIs and metrics that need to be monitored regularly.
*   **Limit Visuals per Page (Reports):**  Avoid overcrowding report pages with too many visuals.  Keep pages focused and easy to understand.  Consider using multiple report pages for different aspects of analysis.
*   **Use Visual Interactions Purposefully:**  Design visual interactions to enhance data exploration and guide users to insights.  Don't overuse interactions if they don't add value.
*   **Ensure Performance:**  Optimize your data model and DAX calculations to ensure reports and dashboards load and interact quickly, especially with large datasets.
*   **Test and Iterate:**  Get feedback from users on your reports and dashboards.  Iterate and refine them based on feedback to improve usability and effectiveness.
*   **Mobile-Friendly Design:**  Consider how your reports and dashboards will look and function on mobile devices.  Power BI Service offers mobile-optimized views.

## Practice Building Interactive Reports and Dashboards

Now it's your turn to build your own interactive reports and dashboards!

1.  **Create a Power BI Report:**  Open your Power BI project (or create a new one).
2.  **Build a Multi-Visual Report Page:**  Create a report page with several different types of basic visuals (charts, tables, cards).
3.  **Add Slicers:**  Add slicers to your report page to allow for interactive filtering.
4.  **Customize Visual Interactions:**  Experiment with editing visual interactions to control how visuals filter and highlight each other.
5.  **Implement Drill-Down and Drill-Through:**  Add drill-down to hierarchical visuals and create a drill-through page for detailed data exploration.
6.  **Publish to Power BI Service:**  Publish your report to your Power BI Service workspace.
7.  **Create a Dashboard:**  Pin key visuals from your report to a new Power BI dashboard.
8.  **Arrange and Customize Dashboard:**  Arrange tiles on your dashboard, resize them, and add text or image tiles to enhance your dashboard.
9.  **Explore Interactivity in Power BI Service:**  View your report and dashboard in the Power BI Service and test their interactivity.

By practicing building interactive reports and dashboards, you'll master the art of creating compelling and user-friendly BI solutions in Power BI! In the next chapter, we'll explore **advanced visualization techniques** to further enhance your reports and dashboards and create even more visually stunning and insightful data stories!
