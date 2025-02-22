# Chapter 15: Power BI Service and Sharing Reports

Welcome to Module 3 conclusion! You've learned how to create amazing reports in Power BI Desktop. Now, it's time to learn how to **share your reports with the world** using the **Power BI Service!**

In this chapter, we'll cover:

*   **What is Power BI Service?** Understanding the cloud-based Power BI Service and its role.
*   **Publishing Reports from Power BI Desktop to Power BI Service:**  Step-by-step guide to publishing your reports.
*   **Navigating the Power BI Service Interface:**  Exploring the key areas of the Power BI Service web interface.
*   **Sharing Reports and Dashboards:**  Different ways to share your Power BI creations with colleagues and stakeholders.
*   **Collaboration in Power BI Service:**  Working together on reports and dashboards with team members.
*   **Data Refresh in Power BI Service:**  Setting up scheduled data refresh to keep your reports up-to-date.
*   **Power BI Mobile Apps:**  Accessing and viewing reports on mobile devices.

## What is Power BI Service?

**Power BI Service is a cloud-based platform from Microsoft for publishing, sharing, collaborating on, and consuming Power BI reports and dashboards.**

Think of Power BI Service as the online home for your Power BI creations. It's where your reports go to become accessible to others and where users can interact with and consume your data insights.

**Key Capabilities of Power BI Service:**

*   **Publishing Reports:**  Publish reports created in Power BI Desktop to the cloud service.
*   **Sharing and Collaboration:**  Share reports and dashboards with colleagues, teams, and external users. Collaborate on report development with team members.
*   **Viewing and Interacting with Reports:**  Users can access and interact with published reports through web browsers and mobile apps.
*   **Dashboards:**  Create and share dashboards that summarize key metrics from reports.
*   **Data Refresh Scheduling:**  Set up automatic data refresh schedules to keep reports connected to live data sources.
*   **Data Gateways:**  Connect to on-premises data sources securely from the cloud service.
*   **Power BI Apps:**  Package and distribute collections of reports and dashboards as Power BI Apps for wider audiences.
*   **Security and Governance:**  Manage user access, permissions, and data security in a centralized cloud environment.
*   **Power BI Mobile Apps:**  Access Power BI reports and dashboards on iOS, Android, and Windows mobile devices.

**Power BI Desktop vs. Power BI Service:**

*   **Power BI Desktop:**  A **desktop application** (Windows only, with Mac options discussed earlier) used for **report creation and development**.  It's where you connect to data, transform data, build data models, design visualizations, and create reports.  **Primarily for report authors and developers.**
*   **Power BI Service:**  A **cloud-based web service** used for **report publishing, sharing, consumption, and collaboration.**  It's where users access and interact with reports, and where administrators manage Power BI environments.  **For report consumers, collaborators, and administrators.**

**You create reports in Power BI Desktop and then publish them to Power BI Service to share them with others.**

## Publishing Reports to Power BI Service

Publishing a report from Power BI Desktop to Power BI Service is a straightforward process:

1.  **Save Your Report in Power BI Desktop:**  Ensure you have saved your Power BI Desktop report (`.pbix` file).
2.  **Sign In to Power BI Desktop (if not already signed in):**  In Power BI Desktop, in the top-right corner, click "Sign in" and enter your Power BI account credentials (the same account you use for Power BI Service).
3.  **Click "Publish" Button:**  In the **Home Ribbon**, click the **"Publish"** button.
4.  **Select a Workspace:**  The "Publish to Power BI" dialog will appear, prompting you to choose a **workspace** in Power BI Service to publish your report to.
    *   **Workspaces:** Workspaces are collaboration areas in Power BI Service. You'll typically have a "My workspace" (your personal workspace) and potentially shared workspaces for teams or projects.  Choose the appropriate workspace.
5.  **Click "Select":**  Click "Select" to start the publishing process.
6.  **Publishing Progress:** Power BI Desktop will show a progress dialog indicating the report is being published to the Power BI Service.
7.  **Publishing Success Message:**  Once publishing is complete, you'll see a "Success!" message with a link "Open report in Power BI" to directly open your published report in the Power BI Service in your web browser.
8.  **Click "Open report in Power BI" (Optional):** Click the link to open your report in Power BI Service and verify that it has been published correctly.

**What Happens During Publishing?**

When you publish a report, Power BI Desktop uploads the following to the Power BI Service:

*   **Report Layout:**  All report pages, visuals, formatting, and interactive elements you designed in Power BI Desktop.
*   **Data Model:**  The data model (tables, relationships, measures, calculated columns) embedded within your `.pbix` file.
*   **Dataset:**  A dataset is created in Power BI Service based on your data model.  If you used "Import" mode for data connections, the data itself is also uploaded and stored in the dataset. If you used "DirectQuery" mode, the dataset contains metadata and connection information to your data source (data remains in the source).

## Navigating the Power BI Service Interface

Once you've published your report and opened Power BI Service in a web browser, you'll see the Power BI Service interface. Let's take a quick tour of the key areas:

**(Imagine a screenshot of Power BI Service interface here with labels for each section)**

The Power BI Service interface is organized to help you find and manage your Power BI content.  Key areas include:

1.  **Navigation Pane (Left Side):**  The left navigation pane provides access to the main sections of Power BI Service:
    *   **Home:**  Your Power BI Service home page, showing recent content, recommended items, and quick access to create new content.
    *   **Browse:**  Browse and discover content across workspaces and the Power BI organization.
    *   **Create:**  Create new reports, dashboards, dataflows, datasets directly in the Power BI Service (limited creation capabilities compared to Power BI Desktop, primarily for quick reports or dashboards based on existing datasets).
    *   **My workspace / Workspaces:** Access your personal workspace ("My workspace") and shared workspaces you are a member of.  Workspaces are containers for reports, dashboards, datasets, and other Power BI items.
    *   **Apps:**  Access Power BI Apps that have been shared with you.
    *   **Dataflows:**  Manage and create dataflows (reusable data preparation steps).
    *   **Datasets:**  Manage and explore datasets.
    *   **Reports:**  View and manage reports.
    *   **Dashboards:** View and manage dashboards.
    *   **Metrics:** (Premium feature) Create and track metrics and goals.
    *   **Learn:** Access Power BI learning resources and documentation.

2.  **Content Area (Main Area):**  The main content area displays the contents of the section you've selected in the navigation pane. For example, if you select "Reports" in a workspace, the content area will show a list of reports in that workspace.

3.  **Report/Dashboard View:** When you open a report or dashboard, the content area will display the interactive report or dashboard itself.  You can interact with visuals, slicers, filters, and explore the data.

4.  **Top Ribbon (Context-Sensitive):**  The ribbon at the top of the Power BI Service interface is context-sensitive.  It changes based on the section you are in and the item you have selected.  For example, when viewing a report, the ribbon will have options for editing, sharing, exporting, etc.

5.  **Action Bar (Visual Header):**  When you hover over a visual in a report or dashboard, an "Action bar" appears in the top-right corner of the visual.  This action bar provides options specific to that visual, such as:
    *   **Focus mode:**  Expand the visual to full-screen for detailed viewing.
    *   **More options (...):**  Access context-specific options like "Export data," "See records," "Edit," "Pin visual," etc.

## Sharing Reports and Dashboards

Sharing your Power BI reports and dashboards is essential for making your insights accessible to others. Power BI Service offers several ways to share:

**1. Sharing within your Organization (Workspace Access):**

*   **Workspace Collaboration:** The most common way to share within an organization is by granting users access to a **Power BI workspace**.
*   **Workspace Roles:**  You can assign different roles to users in a workspace, controlling their permissions:
    *   **Viewer:**  Can view reports and dashboards but cannot edit content.
    *   **Member:** Can view, edit, and create content within the workspace.
    *   **Contributor:**  Similar to Member, with slightly different permissions related to app publishing.
    *   **Admin:**  Full administrative control over the workspace.
*   **Granting Workspace Access:**
    *   **Workspace Access Settings:**  In the Power BI Service, navigate to the workspace you want to share. Click "Access" (or "Workspace access") in the workspace header.
    *   **Add People or Groups:**  Enter the names or email addresses of users or security groups within your organization that you want to grant access to.
    *   **Choose Role:**  Select the appropriate workspace role (Viewer, Member, Contributor, Admin) for each user or group.
    *   **Click "Add":**  Click "Add" to grant access.
*   **Users with workspace access can then access all content within that workspace (reports, dashboards, datasets, etc.), based on their assigned role.**

**2. Sharing Reports and Dashboards Directly (Link Sharing):**

*   **Share Button:**  Open the report or dashboard you want to share in Power BI Service. Click the **"Share"** button in the report/dashboard header.
*   **Share Report/Dashboard Dialog:**  The "Share report" or "Share dashboard" dialog will appear.
    *   **People, groups, or apps:**  Enter the names or email addresses of specific users or groups to share with.
    *   **Permissions:**  Choose permissions:
        *   **Read:**  Users can view the report/dashboard.
        *   **Read and reshare:** Users can view and also reshare the report/dashboard with others.
        *   **Build permission (for reports):**  Allows users to build new reports based on the underlying dataset (for reports only).
    *   **Options:**
        *   **Allow recipients to share this report:**  (If "Read and reshare" permission is selected).
        *   **Send an email notification:**  Optionally send an email notification to recipients with a link to the report/dashboard.
    *   **Click "Grant access" or "Share":**  Click the button to share.
*   **Link Sharing Creates a Direct Link:**  Link sharing creates a direct link to the report or dashboard that you can share with specific individuals.  It's useful for sharing with a smaller, defined audience.

**3. Publishing Reports as Power BI Apps (for Wider Distribution):**

*   **Power BI Apps:**  Power BI Apps are a way to package and distribute collections of reports and dashboards as a single, branded application.  Apps are designed for wider distribution to larger audiences within or outside your organization.
*   **Creating a Power BI App:**
    *   **Workspace Content:**  Ensure your reports and dashboards are organized within a Power BI workspace.
    *   **Publish App:**  In the Power BI Service, navigate to the workspace. Click **"Publish app"** (or "Create app") in the workspace header.
    *   **App Setup:**  The "App setup" dialog will guide you through configuring your app:
        *   **App details:**  App name, description, logo, theme color.
        *   **Navigation:**  Select which reports and dashboards to include in the app navigation menu.
        *   **Permissions:**  Define who can access the app (entire organization, specific security groups, or individuals).
    *   **Publish App:**  Click "Publish app" to create and publish your Power BI App.
*   **App Users Access via App Link:**  Users access Power BI Apps through a dedicated app link.  Apps provide a more structured and branded experience for report consumption compared to sharing individual reports or dashboards.

**4. Embedding Reports (for External Websites or Applications):**

*   **Embed Codes:**  Power BI allows you to generate embed codes for reports and visuals that you can embed into external websites, web applications, SharePoint pages, or other platforms.
*   **Generate Embed Code:**  Open the report you want to embed in Power BI Service.  Go to **File -> Embed report -> Website or portal**.  Choose embed code options (e.g., page to embed, filter pane visibility).  Copy the generated embed code.
*   **Embed in Web Page:**  Paste the embed code into the HTML code of your website or web application.
*   **Embedding Considerations:**
    *   **Security:**  Be mindful of data security and access control when embedding reports externally.  Ensure appropriate authentication and authorization are in place.
    *   **Licensing:**  Users accessing embedded reports may require Power BI licenses depending on the embedding scenario and licensing model.

## Collaboration in Power BI Service

Power BI Service facilitates collaboration among team members working on reports and dashboards:

*   **Workspace Collaboration (as discussed earlier):**  Workspaces are the primary collaboration environment.  Team members with "Member," "Contributor," or "Admin" roles can work together on reports, datasets, and dashboards within a workspace.
*   **Shared Datasets:**  Teams can collaborate on data models by using **shared datasets**.  One team member can create and publish a dataset to a workspace, and other team members can then build reports and dashboards based on that shared dataset, promoting data model consistency and reusability.
*   **Report Co-authoring (in Power BI Desktop - Preview feature at the time of writing):**  Power BI Desktop is introducing co-authoring capabilities, allowing multiple authors to work on the same report file simultaneously (similar to co-authoring in Microsoft Office documents).  Check Power BI documentation for the latest status of co-authoring features.
*   **Comments and Annotations:**  Users can add comments and annotations directly to reports and dashboards in Power BI Service to discuss data insights, ask questions, and collaborate on analysis.

## Data Refresh in Power BI Service

To keep your Power BI reports and dashboards up-to-date with the latest data, you need to set up **data refresh** in Power BI Service.  Data refresh schedules depend on your data connection mode and data source type.

**Data Refresh for Import Mode Datasets:**

*   **Scheduled Refresh:**  For datasets using "Import" mode, you need to configure **scheduled refresh** in Power BI Service.  This tells Power BI Service to periodically connect to your data source and refresh the data in your dataset.
*   **Dataset Settings -> Schedule Refresh:**  In Power BI Service, navigate to the workspace containing your dataset.  Find your dataset in the "Datasets" section.  Click the ellipsis (...) next to the dataset name and choose "Settings."  Go to the "Schedule refresh" section in the dataset settings.
*   **Configure Refresh Schedule:**
    *   **Data source credentials:**  You may need to configure or verify data source credentials to allow Power BI Service to connect to your data source.
    *   **Refresh schedule:**  Enable scheduled refresh and set the refresh frequency (daily, weekly, etc.) and time slots for refresh.  Refresh frequency depends on your Power BI license and data source capabilities.
    *   **Apply Changes:**  Save your refresh schedule settings.
*   **Gateway for On-Premises Data Sources:**  If your data source is on-premises (e.g., on a local server or database within your organization's network), you'll need to set up a **Power BI Gateway**.  The gateway acts as a secure bridge allowing Power BI Service in the cloud to connect to your on-premises data source for data refresh.  Gateway setup is a more advanced topic, refer to Power BI documentation for detailed gateway setup guides.

**Data Refresh for DirectQuery Datasets:**

*   **No Scheduled Refresh (Typically):**  For datasets using "DirectQuery" mode, data is not imported and stored in Power BI.  Instead, Power BI queries the data source directly whenever a report or visual is loaded or interacted with.  Therefore, **scheduled refresh is generally not needed** for DirectQuery datasets, as they always show the latest data from the source.
*   **Consider Gateway for On-Premises DirectQuery:**  If your DirectQuery data source is on-premises, you'll still need to configure a Power BI Gateway to enable Power BI Service to connect to your on-premises data source for live querying.

**Manual Refresh:**

You can also trigger a **manual data refresh** at any time for both Import and DirectQuery datasets:

*   **Dataset Actions -> Refresh Now:**  In Power BI Service, find your dataset in the "Datasets" section.  Click the ellipsis (...) next to the dataset name and choose "Refresh now."  This will initiate an immediate data refresh.

## Power BI Mobile Apps

Power BI Mobile apps (available for iOS, Android, and Windows) allow you to access and view your Power BI reports and dashboards on mobile devices.

*   **Download from App Stores:**  Download the Power BI Mobile app from the App Store (iOS), Google Play Store (Android), or Microsoft Store (Windows).
*   **Sign In:**  Sign in to the Power BI Mobile app using your Power BI account credentials.
*   **Browse and View Content:**  The mobile app provides a mobile-optimized view of your Power BI Service content (reports, dashboards, workspaces, apps).  You can browse, view, and interact with reports and dashboards on your mobile device.
*   **Interactive Features:**  Mobile apps support touch interactions, drill-down, filtering, annotations, and other interactive features for data exploration on the go.
*   **Offline Access (Limited):**  Power BI Mobile apps offer some limited offline access to recently viewed reports and dashboards.

## Practice Publishing and Sharing Reports

Now it's your turn to practice publishing and sharing your Power BI reports and dashboards!

1.  **Publish a Report to Power BI Service:**  Publish one of your Power BI Desktop reports to your "My workspace" in Power BI Service.
2.  **Explore Power BI Service Interface:**  Navigate the Power BI Service web interface.  Explore the "Home," "Browse," "Workspaces," "Reports," and "Dashboards" sections.  Find your published report.
3.  **Share Your Report with a Colleague (Link Sharing):**  Share your published report with a colleague or friend using the "Share" link.
4.  **Grant Workspace Access:**  Grant a colleague "Viewer" access to your "My workspace."  Have them access the workspace and view your report.
5.  **Create a Dashboard and Pin Visuals:**  Create a new dashboard in Power BI Service and pin a few key visuals from your published report to the dashboard.
6.  **View Dashboard and Report in Power BI Service:**  View your report and dashboard in Power BI Service and test their interactivity.
7.  **Explore Power BI Mobile App:**  Download and install the Power BI Mobile app on your mobile device.  Sign in and access your published report and dashboard on your mobile device.
8.  **(Optional) Set up Data Refresh (if applicable):**  If you are using "Import" mode with a data source you can refresh, try setting up a scheduled data refresh for your dataset in Power BI Service.

By practicing publishing, sharing, and exploring Power BI Service, you'll complete your journey from report creation in Power BI Desktop to sharing your insights with the world through the Power BI cloud platform!  Congratulations on completing Module 3: Data Visualization and Reporting!  You are now well-equipped to create and share powerful Power BI reports and dashboards!  In Module 4, we'll dive into **Advanced Power BI Features**, exploring topics like Power BI and AI, Python/R integration, performance tuning, and administration!
