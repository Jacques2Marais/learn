# Chapter 3: Connecting to Data Sources

Power BI's true power lies in its ability to connect to a vast universe of data sources.  In this chapter, we'll explore how to bring your data into Power BI Desktop and start your data analysis journey.

## The "Get Data" Experience

The gateway to connecting to data in Power BI is the **"Get Data"** feature. You'll find the "Get Data" button prominently displayed in several places:

*   **On the Home Ribbon:** In Power BI Desktop, the "Home" ribbon has a "Data" group, and within it, you'll see the "Get Data" button.
*   **In the "Get started" screen:** When you first launch Power BI Desktop, you'll often see a "Get started" screen with common tasks, including "Get data."
*   **From the "File" Menu:** You can also access "Get Data" through the "File" menu, usually under "Import" or "Get Data."

Clicking "Get Data" opens the **"Get Data" dialog box**. This is your central hub for choosing your data source.

**(Imagine a screenshot of the "Get Data" dialog box here, categorized and with search bar)**

## Exploring Data Source Categories

The "Get Data" dialog box neatly organizes data sources into categories to help you find what you need quickly.  Here are the main categories you'll encounter:

*   **All:** This category lists all available data sources in alphabetical order.  Useful if you know the name of your data source but not its category.
*   **File:** This category is for connecting to data stored in files on your computer or network. Common file types include:
    *   **Excel Workbook:** Connect to data in `.xlsx` and `.xls` files.
    *   **CSV (Comma Separated Values) Text:** Connect to data in `.csv` files.
    *   **Text/CSV:**  Another option for text-based files, sometimes offering slightly different import options.
    *   **XML:** Connect to data in `.xml` files.
    *   **JSON:** Connect to data in `.json` files.
    *   **Folder:** Connect to all files within a folder, useful for processing multiple files with the same structure.
    *   **PDF:**  Extract data from `.pdf` documents (Power BI will attempt to recognize tables).
    *   **SharePoint folder:** Connect to files stored in SharePoint folders.

*   **Database:** This category is for connecting to various types of databases.  Power BI supports a wide range of database systems, including:
    *   **SQL Server database:** Microsoft SQL Server.
    *   **Access database:** Microsoft Access databases (`.accdb`, `.mdb`).
    *   **MySQL database:** Popular open-source database.
    *   **PostgreSQL database:** Another popular open-source database.
    *   **Oracle database:** Enterprise-grade database.
    *   **IBM Db2 database:** IBM's database system.
    *   **Teradata Database:**  Data warehousing database.
    *   **And many more!** Scroll through the list to see the extensive database support.

*   **Power BI:** This category is for connecting to other Power BI components and services:
    *   **Power BI datasets:** Connect to existing datasets published to the Power BI Service.  Allows you to build reports on top of existing data models.
    *   **Power BI dataflows:** Connect to dataflows, which are reusable data preparation and transformation steps in the Power BI Service.

*   **Azure:**  This category lists various Azure cloud services as data sources:
    *   **Azure SQL Database:** Microsoft's cloud-based SQL Server.
    *   **Azure Synapse Analytics:**  Data warehousing and big data analytics service.
    *   **Azure Analysis Services:**  Cloud-based analytical data engine.
    *   **Azure Blob Storage:**  Scalable object storage for unstructured data.
    *   **Azure Data Lake Storage Gen2:**  Data lake storage optimized for big data analytics.
    *   **And many other Azure services.**

*   **Online Services:** This category provides connectors to various online services and platforms:
    *   **SharePoint Online list:** Connect to lists in SharePoint Online.
    *   **Microsoft Exchange Online:** Connect to data from Exchange Online.
    *   **Dynamics 365:** Connect to data from Microsoft Dynamics 365 applications.
    *   **Salesforce:** Connect to Salesforce CRM data.
    *   **Google Analytics:** Connect to website analytics data from Google Analytics.
    *   **Adobe Analytics:** Connect to Adobe Analytics data.
    *   **Facebook:** Connect to Facebook Pages data (limited access due to API changes).
    *   **And many more online services!**

*   **Other:** This "catch-all" category includes less common or specialized data sources:
    *   **Web:** Connect to data from websites via web scraping or APIs (use with caution and respect website terms of service).
    *   **ODBC (Open Database Connectivity):**  Connect to data sources using ODBC drivers.
    *   **OLE DB (Object Linking and Embedding Database):** Connect to data sources using OLE DB providers.
    *   **Blank query:** Start with a blank Power Query Editor window to manually build your data query from scratch (more advanced).

## Connecting to Common Data Sources: Examples

Let's walk through connecting to a few common data source types:

### 1. Connecting to an Excel Workbook

Excel is a ubiquitous tool, and often the starting point for data analysis.

1.  **Click "Get Data"** and choose **"Excel Workbook"** from the "File" category (or search for "Excel").
2.  **Browse** to the location of your Excel file and **select it.** Click **"Open."**
3.  **Navigator Dialog:** Power BI will open a "Navigator" dialog box. This dialog displays the worksheets and tables found within your Excel workbook.
4.  **Select Items:**  **Check the boxes** next to the worksheets or tables you want to import into Power BI. You can preview the data by clicking on an item.
5.  **Choose Load or Transform Data:**
    *   **Load:** Click "Load" to directly import the selected data into your Power BI data model.  Choose this if your data is already clean and ready for analysis.
    *   **Transform Data:** Click "Transform Data" to open the Power Query Editor. This is highly recommended! Power Query Editor allows you to clean, shape, and transform your data *before* it's loaded into Power BI.  We'll explore Power Query Editor in detail in the next chapter.

### 2. Connecting to a CSV File

CSV (Comma Separated Values) files are another common format for storing tabular data.

1.  **Click "Get Data"** and choose **"Text/CSV"** from the "File" category (or search for "CSV").
2.  **Browse** to your CSV file and **select it.** Click **"Open."**
3.  **Preview and Settings:** Power BI will display a preview of your CSV data and show import settings.
    *   **Delimiter:**  Power BI usually auto-detects the delimiter (comma, semicolon, tab, etc.).  Verify it's correct.
    *   **Data Type Detection:** Power BI attempts to automatically detect data types for each column (e.g., text, number, date). Review and adjust if needed.
    *   **Encoding:**  Choose the correct file encoding if you encounter issues with character display (usually "UTF-8" is a good default).
4.  **Choose Load or Transform Data:**  As with Excel, decide whether to "Load" directly or "Transform Data" using Power Query Editor.  Transforming is generally recommended.

### 3. Connecting to a Database (SQL Server Example)

Connecting to databases requires you to provide connection details.  Let's use SQL Server as an example.

1.  **Click "Get Data"** and choose **"SQL Server database"** from the "Database" category (or search for "SQL Server").
2.  **SQL Server Database Dialog:** A dialog box will appear asking for connection information:
    *   **Server:** Enter the name of your SQL Server instance. This might be a server name, IP address, or hostname.
    *   **Database (Optional):** You can optionally specify a database name to connect to a specific database on the server. If left blank, you'll connect to the server and can choose databases later.
    *   **Data Connectivity Mode:**
        *   **Import:**  Power BI will import a copy of the data from the database into your Power BI data model.  This is the most common mode.
        *   **DirectQuery:** Power BI will query the database directly *every time* you interact with a visual.  DirectQuery is useful for very large datasets or real-time data, but can impact performance. We'll discuss DirectQuery in more detail in a later chapter.  For now, **"Import" is recommended.**
3.  **Credentials (if required):** Depending on your SQL Server setup, you may be prompted to enter credentials (username and password) to access the database. Choose the appropriate authentication method (e.g., Windows Authentication, Database Authentication).
4.  **Navigator Dialog:**  Once connected, the "Navigator" dialog will appear, showing the databases (if you didn't specify one earlier), tables, and views available in the SQL Server.
5.  **Select Tables/Views:**  **Check the boxes** next to the tables or views you want to import.  Preview the data.
6.  **Choose Load or Transform Data:**  Decide whether to "Load" or "Transform Data."  Transforming is usually a good practice.

## Connection Modes: Import vs. DirectQuery

As mentioned in the SQL Server example, Power BI offers two main data connectivity modes:

*   **Import:**
    *   **Data is copied** from the data source and stored within the Power BI data model.
    *   **Faster performance** for visualizations and reports, as data is readily available in memory.
    *   **Data refresh is required** to update the data in Power BI with changes from the source. You can schedule automatic refreshes in the Power BI Service.
    *   **Most common and recommended mode** for most scenarios.

*   **DirectQuery:**
    *   **Data is not imported.** Power BI sends queries directly to the data source to retrieve data *on demand* when you interact with visuals.
    *   **Real-time data:**  Visuals always show the latest data from the source.
    *   **Can handle very large datasets** that might not fit into Power BI's memory limits.
    *   **Slower performance** compared to Import, as each visual interaction triggers a database query. Performance depends heavily on the data source's speed and query optimization.
    *   **Limitations on DAX and Power Query features** compared to Import mode.
    *   **More complex to set up and manage.**

**When to use Import vs. DirectQuery:**

*   **Use Import when:**
    *   Performance is a priority.
    *   Data volume is manageable within Power BI's limits.
    *   You need to perform complex data modeling and DAX calculations.
    *   Data doesn't need to be absolutely real-time (near real-time with scheduled refresh is sufficient).

*   **Use DirectQuery when:**
    *   You need to visualize very large datasets that exceed Power BI's memory capacity.
    *   Real-time data is critical and you need to see the absolute latest data in visuals.
    *   You are connecting to a data source with strong query performance.
    *   You understand the limitations of DirectQuery and are willing to work within them.

For beginners and most common BI scenarios, **Import mode is the recommended and easier choice.**

## Practice Connecting to Data

Now it's your turn!  Experiment with connecting to different data sources using the "Get Data" feature in Power BI Desktop. Try connecting to:

*   An Excel file you have on your computer.
*   A CSV file (you can find sample CSV datasets online).
*   If you have access to a database (like SQL Server, MySQL, etc.), try connecting to it in Import mode.

Get comfortable with the "Get Data" dialog, explore the different categories, and practice selecting data and choosing between "Load" and "Transform Data."

In the next chapter, we'll dive into the powerful **Power Query Editor** and learn how to transform and shape your data to get it ready for amazing analysis and visualizations!
