# Chapter 14: Custom Visuals and Themes

In this chapter, we'll explore how to take the visual appeal and branding of your Power BI reports to the next level by leveraging **Custom Visuals and Themes**.

## Custom Visuals: Expanding Your Visualization Library

As introduced in the previous chapter, **Custom Visuals** provide a way to extend Power BI's built-in visualization library. They offer specialized chart types, industry-specific visuals, and enhanced visual aesthetics beyond the standard visuals.

**Power BI Visuals Marketplace:**

The primary source for custom visuals is the **Power BI Visuals Marketplace**, accessible directly from Power BI Desktop and the Power BI Service.

*   **Vast Library:** The marketplace offers a vast and growing library of custom visuals, created by Microsoft, certified partners, and the Power BI community.
*   **Categories and Search:** Visuals are categorized (charts, maps, gauges, etc.) and searchable by keyword, making it easy to find visuals for specific needs.
*   **Previews and Descriptions:** Each visual listing includes previews, descriptions, documentation links, and user reviews to help you evaluate visuals before importing them.
*   **Certification:** Some visuals are "Power BI Certified," indicating they have undergone testing and meet certain quality and security standards from Microsoft. Certified visuals are generally recommended for production reports.

**Importing and Using Custom Visuals:**

1.  **Get More Visuals:**
    *   **In Power BI Desktop:** In the "Visualizations" pane, click the ellipsis (...) and select "Get more visuals."
    *   **In Power BI Service:** When editing a report in the Power BI Service, look for the "Import a custom visual" option in the "Visualizations" pane.
2.  **Browse and Search Marketplace:** The Power BI Visuals marketplace dialog will open. Browse categories or use the search bar to find visuals you need.
3.  **Preview and Select Visual:** Click on a visual listing to see a larger preview, read the description, and review details.
4.  **Add Visual to Report:** Click the "Add" button on a visual listing to import it into your current Power BI report.
5.  **Visual Appears in Visualizations Pane:** The imported custom visual icon will appear as a new visual type in your "Visualizations" pane, ready to be used like any built-in visual.

**Types of Custom Visuals Available:**

The Power BI Visuals Marketplace offers a diverse range of custom visuals, including but not limited to:

*   **Advanced Charts:**
    *   **Network Diagrams (Force-Directed Graphs):** Visualizing relationships and connections between entities.
    *   **Gantt Charts:** Project scheduling and timeline visualization.
    *   **Bullet Charts:**  Comparing a metric to a target and performance bands.
    *   **Advanced Time Series Charts:**  Specialized charts for time series analysis and forecasting.
    *   **Sankey Diagrams:**  Visualizing flow and distribution of quantities through different stages.
    *   **Chord Diagrams:**  Showing relationships between entities in a circular layout.
*   **Industry-Specific Visuals:**
    *   **Financial Charts (Candlestick Charts, OHLC Charts):**  For financial data analysis.
    *   **Manufacturing Process Visuals:**  Visualizing manufacturing workflows and processes.
    *   **Healthcare Dashboards Visuals:**  Visuals tailored for healthcare data and KPIs.
    *   **Marketing Analytics Visuals:**  Visuals for marketing campaign performance and customer segmentation.
*   **Visually Enhanced and Interactive Visuals:**
    *   **Animated Charts:**  Visuals with animations to highlight trends and changes over time.
    *   **Interactive Storytelling Visuals:**  Visuals designed for guided data exploration and storytelling.
    *   **Enhanced Tables and Matrices:**  Customizable tables and matrices with advanced formatting and features.

**Considerations When Using Custom Visuals:**

*   **Certification:**  Prioritize using "Power BI Certified" visuals, especially for production reports, as they offer a higher level of quality and security assurance.
*   **Functionality and Suitability:**  Evaluate if a custom visual truly adds value to your report and effectively addresses your visualization needs. Don't use custom visuals just for the sake of using them.
*   **Performance:**  Test the performance of custom visuals, especially with large datasets. Some custom visuals might be less performant than built-in visuals.
*   **Usability and Learning Curve:**  Consider the learning curve for users to understand and interact with custom visuals. Ensure they are intuitive and well-documented.
*   **Mobile Compatibility:**  Check if custom visuals are mobile-friendly and render correctly on mobile devices if mobile report viewing is important.
*   **Support and Updates:**  Be aware that custom visuals are maintained by third-party developers. Support and update frequency may vary. Check the visual listing for developer information and support resources.

## Themes: Consistent Design and Branding

**Power BI Themes** provide a powerful way to apply consistent visual styling and branding across your entire report. Themes control colors, fonts, visual styles, chart defaults, and other visual elements, ensuring a cohesive and professional look for your reports.

**Benefits of Using Themes:**

*   **Consistent Design:**  Apply a uniform visual style across all report pages and visuals, creating a professional and polished look.
*   **Branding:**  Incorporate your organization's branding (colors, fonts, logo) into your Power BI reports to reinforce brand identity.
*   **Efficiency and Time Savings:**  Apply a theme once, and it automatically styles all visuals in your report, saving time and effort compared to formatting each visual individually.
*   **Accessibility:**  Themes can be designed to improve report accessibility by ensuring sufficient color contrast and readability for users with visual impairments.
*   **Customization and Flexibility:**  Power BI themes are highly customizable. You can use built-in themes, customize existing themes, or create your own custom themes from scratch.

**Types of Themes in Power BI:**

*   **Built-in Themes:** Power BI Desktop comes with a gallery of pre-designed built-in themes. These themes offer various color palettes, font styles, and visual styles to quickly change the overall look of your report.
*   **Custom Themes (JSON Files):**  For advanced customization, you can create your own custom themes by defining theme settings in a JSON (JavaScript Object Notation) file. This allows for granular control over every aspect of report styling.
*   **Theme Gallery (Online):**  The Power BI Theme Gallery (online) provides a collection of community-created custom themes that you can download and import into Power BI Desktop.

**Applying Built-in Themes:**

1.  **View Ribbon -> Themes:** In Power BI Desktop, go to the "View" ribbon. In the "Themes" group, you'll see the "Themes" dropdown gallery.
2.  **Browse and Select Theme:**  Browse through the theme gallery and click on a theme thumbnail to apply it to your current report.
3.  **Theme Preview:** Power BI will instantly apply the selected theme, and you'll see how it changes the colors, fonts, and styles of all visuals in your report.
4.  **"More Themes" -> "Theme gallery":**  Click "Theme gallery" to explore more themes online in the Power BI Theme Gallery.

**Customizing Built-in Themes:**

You can customize a built-in theme to adjust it to your specific preferences or branding:

1.  **View Ribbon -> Themes -> Customize current theme:**  Click "Customize current theme" in the "Themes" dropdown.
2.  **Customize Theme Dialog:** The "Customize theme" dialog will open, allowing you to customize various theme settings:
    *   **Colors:**
        *   **Name and Colors:**  Change the theme name and adjust the primary theme colors (e.g., "Accent 1," "Accent 2," "Neutral dark," "Neutral primary").
        *   **Advanced color settings:**  Customize more detailed color settings for data colors, background, text, and visuals.
    *   **Text:**
        *   **General text:**  Set default font family, size, and color for all text elements in the report.
        *   **Title, Header, Card and KPI:** Customize font styles for specific text elements.
    *   **Visuals:**
        *   **Visual styles:**  Control default styles for visuals (background, border, header, tooltips).
        *   **Chart styles:**  Customize default styles for charts (data colors, data labels, axes, gridlines, legend).
        *   **Filter pane:**  Customize the style of the filter pane.
    *   **Page:**
        *   **Page background:**  Set the default page background color or image.
        *   **Wallpaper:** Set the report wallpaper (background behind the page).
    *   **Filter pane:** Customize the appearance of the filter pane.
3.  **Apply and Save Changes:**  Make your desired customizations in the dialog and click "Apply" to apply the changes to your report. You can also "Save" the customized theme as a new custom theme file (.json) for reuse.

**Creating Custom Themes (JSON Files):**

For the most granular control over report styling, you can create your own custom themes by editing a **JSON theme file**.

1.  **Export Current Theme (Optional Starting Point):**  You can start by exporting the JSON file of a built-in theme or a customized theme as a starting point.  Go to **View Ribbon -> Themes -> Save current theme** to export the current theme as a .json file.
2.  **Edit JSON File:**  Open the exported .json file (or create a new .json file from scratch) in a text editor or JSON editor (like VS Code).
3.  **Theme JSON Structure:**  Theme JSON files follow a specific structure, defining various properties under different sections:
    *   `name`: Theme name.
    *   `visualStyles`:  Defines styles for different visual types (card, chart, slicer, etc.).  You can customize properties like `*`.`categoryAxis`, `*`.`dataLabels`, `*`.`fill`, `*`.`title`, etc.  (Refer to Power BI Theme JSON documentation for detailed property options).
    *   `colors`: Defines the color palette for the theme.
    *   `textClasses`: Defines text styles for different text elements (title, header, label, etc.).
    *   `dataColors`: Defines data colors for charts.
    *   `backgrounds` and `foregrounds`: Defines background and foreground colors.
    *   `visualContainers`: Defines styles for visual containers (borders, backgrounds).
    *   `page`: Defines page-level styles (background, wallpaper).
    *   `filterCard`: Defines styles for filter cards.

4.  **Import Custom Theme:**  To use your custom theme JSON file, go to **View Ribbon -> Themes -> Browse for themes**.  Select your .json theme file to import and apply it.

**Tips for Creating Effective Themes:**

*   **Brand Guidelines:**  Align your theme with your organization's brand guidelines (colors, fonts, logo).
*   **Color Palette:**  Choose a color palette that is visually appealing, harmonious, and appropriate for your data and audience. Consider using color palettes from color theory resources or branding guidelines.
*   **Font Selection:**  Select readable and professional fonts. Limit the number of font families used in a report for consistency.
*   **Visual Consistency:**  Maintain visual consistency across all report pages and visuals by using themes effectively.
*   **Accessibility Considerations:**  Design themes with accessibility in mind. Ensure sufficient color contrast for text and data elements to be readable by users with visual impairments. Use appropriate font sizes and avoid overly complex or distracting visual styles.
*   **Theme Testing:**  Test your theme on different report types and with various data scenarios to ensure it works well in different contexts.  Get feedback from other users on your theme design.

## Practice Custom Visuals and Themes

Now it's your turn to practice using custom visuals and themes to enhance your Power BI reports!

1.  **Explore Power BI Visuals Marketplace:**  Browse the Power BI Visuals Marketplace and identify a few custom visuals that seem interesting or potentially useful for your reporting needs.
2.  **Import and Experiment with Custom Visuals:**  Import a few custom visuals into Power BI Desktop and experiment with using them in a report.  Try different data field mappings and formatting options.
3.  **Apply Built-in Themes:**  Apply different built-in themes to your Power BI reports and observe how they change the overall look and feel.
4.  **Customize a Built-in Theme:**  Customize a built-in theme by adjusting colors, fonts, and visual styles in the "Customize theme" dialog. Save your customized theme.
5.  **(Optional) Create a Basic Custom Theme JSON File:**  Try creating a basic custom theme JSON file by modifying an exported theme JSON or creating one from scratch.  Focus on customizing colors and fonts initially.  Import and apply your custom theme JSON file to Power BI Desktop.
6.  **Compare Themed vs. Un-themed Reports:**  Create two versions of the same report: one with a well-designed theme and one without.  Compare the visual impact and user experience of the themed vs. un-themed report.

By practicing with custom visuals and themes, you'll gain the skills to create visually stunning, branded, and user-friendly Power BI reports that effectively communicate data insights and enhance the overall BI experience! In the next chapter, we'll move on to **Power BI Service and Sharing Reports**, where you'll learn how to publish, share, and collaborate on your Power BI creations with others!
