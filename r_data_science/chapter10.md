# Chapter 10: Deploying R Data Science Projects

Welcome to the final chapter: Deploying R Data Science Projects! This chapter focuses on sharing your R data science work with the world. We'll cover creating R packages, reproducible research and reporting with R Markdown, and an introduction to deploying R applications.

## Creating R Packages

Creating R packages is a way to organize, document, and share your R code, functions, and datasets. Packages make your code reusable, reproducible, and easier to distribute to others.

### Basic R Package Structure

A basic R package directory structure typically includes:

*   **`DESCRIPTION` file:**  Metadata about the package (name, version, title, author, description, dependencies, license, etc.).
*   **`NAMESPACE` file:**  Specifies exported and imported functions and objects.
*   **`R/` directory:**  Contains your R code files (`.R` files) with functions and code.
*   **`man/` directory:**  Contains documentation files (`.Rd` files) for functions and datasets.
*   **`data/` directory:**  (Optional) Contains datasets used in your package (`.rda` files).
*   **`tests/` directory:** (Optional) Contains unit tests for your package code.

### Creating a Package with `devtools`

`devtools` package simplifies R package development.

*   **Install `devtools` if needed:** `install.packages("devtools")`

*   **Create a package skeleton:** Use `create_package()` function.

    ```R
    library(devtools)

    # Create a new package directory (e.g., "mypackage") in your working directory
    create_package("mypackage")

    # This will create a directory "mypackage" with the basic package structure.
    # Navigate into the "mypackage" directory in your file explorer.
    ```

*   **Edit `DESCRIPTION` file:** Open `mypackage/DESCRIPTION` and fill in the package metadata (Title, Version, Description, Author, Maintainer, License, etc.).

*   **Add functions to `R/` directory:** Create `.R` files in the `R/` directory (e.g., `R/myfunctions.R`) and write your R functions in these files.

    **Example `R/myfunctions.R`:**

    ```R
    # R functions for your package

    #' Add two numbers
    #'
    #' This function adds two numbers.
    #'
    #' @param a The first number.
    #' @param b The second number.
    #' @return The sum of a and b.
    #' @examples
    #' add_numbers(5, 3)
    #' @export
    add_numbers <- function(a, b) {
      return(a + b)
    }

    #' Multiply two numbers
    #'
    #' This function multiplies two numbers.
    #'
    #' @param x The first number.
    #' @param y The second number.
    #' @return The product of x and y.
    #' @export
    multiply_numbers <- function(x, y) {
      return(x * y)
    }
    ```

    *   **Documentation comments:**  Use roxygen2-style documentation comments (starting with `#'`) above each function to document functions, parameters, and return values. `@export` tag makes the function available to users of your package.

*   **Document your package:**  Use `document()` function from `devtools` to generate documentation (`.Rd` files in `man/` directory) from roxygen2 comments and update `NAMESPACE`.

    ```R
    setwd("mypackage") # Set working directory to package root
    document() # Generate documentation and update NAMESPACE
    ```

*   **Build and Install your package:** Use `build()` and `install()` functions.

    ```R
    build() # Build package (creates .tar.gz file)
    install() # Install package locally
    ```

    After installation, you can load your package using `library(mypackage)` and use your functions.

*   **Check your package:**  Use `check()` function to run package checks (style, documentation, tests, etc.).

    ```R
    check() # Run package checks
    ```

    Address any warnings or errors reported by `check()`.

### Adding Datasets and Tests (Optional)

*   **Datasets:**  Put datasets in the `data/` directory as `.rda` files. Document them in roxygen2 comments in an R file (e.g., `R/data.R`) with `@export` and `@docType data` tags. Use `load("data/your_dataset.rda")` to load data in your functions or examples.
*   **Tests:**  Write unit tests in the `tests/testthat/` directory using `testthat` package. Use `test()` function from `devtools` to run tests.

### Sharing your Package

*   **CRAN (Comprehensive R Archive Network):**  For wider distribution, you can submit your package to CRAN after it passes all checks and meets CRAN policies. CRAN submission process involves thorough checks and review.
*   **GitHub:**  Share your package on GitHub for version control, collaboration, and easier installation using `devtools::install_github()`.
*   **Personal Website/Repository:**  Host your package files on your website or a personal repository for direct download and installation.

## Reproducible Research and Reporting with R Markdown

R Markdown is a powerful tool for creating dynamic, reproducible reports and documents that combine text, code, and output (tables, plots, etc.) in a single document. It's excellent for sharing your data analysis and research findings.

### Basic R Markdown Structure

An R Markdown file (`.Rmd`) is a plain text file with a combination of:

*   **Markdown text:**  For writing narrative, explanations, and formatting text (headings, lists, links, etc.).
*   **Code chunks:**  For embedding R code to be executed. Code chunks are enclosed in `````{r} ````` blocks.

### Creating an R Markdown Document

1.  **Create a new R Markdown file in RStudio:** File -> New File -> R Markdown. Choose output format (HTML, PDF, Word, etc.).
2.  **Edit the `.Rmd` file:** Write your document content using Markdown and R code chunks.

**Example `.Rmd` file:**

```markdown
---
title: "Iris Data Analysis Report"
author: "Your Name"
date: "February 23, 2025"
output: html_document
---

## Introduction

This report analyzes the classic `iris` dataset.

## Data Summary

```{r data-summary}
# R code chunk for data summary
summary(iris)
```

## Scatter Plot

```{r scatter-plot}
# R code chunk for scatter plot
library(ggplot2)
ggplot(iris, aes(x = Sepal.Length, y = Sepal.Width, color = Species)) +
  geom_point() +
  labs(title = "Sepal Length vs. Sepal Width")
```

## Conclusion

From the analysis, we can see... (write your conclusions here).

```

### Knitr and Rendering

*   **Knitr:**  R package that processes R Markdown files. It executes R code chunks and weaves together text and output to create the final document.
*   **Rendering (Knitting):**  Click the "Knit" button in RStudio or use `rmarkdown::render("your_document.Rmd")` in the console to render your R Markdown file into the specified output format (e.g., HTML, PDF, Word).

### R Markdown Features

*   **Output Formats:**  Support for various output formats: HTML, PDF, Word, presentations (Beamer, Slidy, ioslides), dashboards, and more.
*   **Code Chunk Options:**  Control how code chunks are executed and displayed (e.g., `echo = TRUE/FALSE` to show/hide code, `eval = TRUE/FALSE` to execute/not execute code, `include = TRUE/FALSE` to include/exclude output, `warning = FALSE`, `message = FALSE`).
*   **Inline R Code:**  Embed R code directly in text using `` `r your_r_code` ``. Example: "The mean sepal length is `` `r mean(iris$Sepal.Length) ` `` cm."
*   **Flexibility:**  Customize document appearance, add citations, bibliographies, themes, and more.
*   **Reproducibility:**  R Markdown documents are reproducible. When you re-render the document, the code is re-executed, ensuring that your results are up-to-date and consistent with your code and data.

## Introduction to Deploying R Applications

Deploying R applications makes your R-based tools and analyses accessible to users through web interfaces or other deployment methods.

### Shiny Apps Deployment

`Shiny` apps (introduced in Chapter 7) are web applications built with R. They can be deployed to make them accessible online.

*   **shinyapps.io:**  RStudio's cloud hosting service for Shiny apps. Easiest way to deploy Shiny apps. Free tier available for limited usage. Paid plans for more resources and features.
    *   **Deploy button in RStudio:**  If you have a Shiny app open in RStudio, click the "Publish" button to deploy to shinyapps.io (requires RStudio Cloud account or shinyapps.io account).
    *   **`rsconnect` package:**  Use `rsconnect::deployApp()` function to deploy programmatically.

*   **Shiny Server (Open Source):**  Set up your own Shiny Server on a server (e.g., cloud instance, local server). More control over server environment. Requires server administration skills.
*   **RStudio Connect (Commercial):**  RStudio's enterprise platform for publishing Shiny apps, R Markdown reports, dashboards, APIs, and more. Collaboration, security, and management features.

### R APIs and Web Services

*   **Plumber package:**  Build web APIs using R code. Expose R functions as API endpoints that can be accessed via HTTP requests. Useful for creating backend services for web applications or integrating R functionality into other systems.
*   **DeployR (Commercial, now discontinued by Microsoft):**  Older platform for deploying R analytics as web services.  Less relevant now, consider Plumber or other API deployment options.

### Docker and Containerization

*   **Docker:**  Containerization platform for packaging applications and their dependencies into containers. Dockerize R applications (Shiny apps, Plumber APIs, R scripts) for consistent and portable deployment across different environments.
*   **Benefits:**  Reproducibility, isolation, scalability, simplified deployment.

### Cloud Platforms (AWS, Google Cloud, Azure)

*   **Cloud Instances (VMs):**  Deploy R applications on virtual machines in cloud platforms (e.g., AWS EC2, Google Compute Engine, Azure VMs).
*   **Container Services (Kubernetes, ECS, etc.):**  Deploy Dockerized R applications on container orchestration platforms in the cloud for scalability and management.
*   **Serverless Functions (AWS Lambda, Google Cloud Functions, Azure Functions):**  For event-driven R code execution in the cloud (e.g., triggered by API requests, data changes).

## Let's Practice!

1.  **R Package Creation:**
    *   Create a new R package using `devtools::create_package()`.
    *   Edit the `DESCRIPTION` file.
    *   Add some R functions to the `R/` directory with roxygen2 documentation.
    *   Document, build, install, and check your package using `devtools` functions.
    *   (Optional) Add a dataset to your package and document it.
2.  **R Markdown Reporting:**
    *   Create a new R Markdown document in RStudio.
    *   Write a report that includes text, R code chunks, plots, and tables based on your previous data analyses (e.g., from `iris` dataset).
    *   Experiment with different output formats (HTML, PDF, Word).
    *   Customize code chunk options and document appearance.
3.  **Shiny App Deployment (Introduction):**
    *   If you created a basic Shiny app in Chapter 7, try deploying it to shinyapps.io using the "Publish" button in RStudio or `rsconnect::deployApp()`.
    *   Explore shinyapps.io dashboard to manage your deployed app.

## Chapter Summary

Congratulations! You've reached the final chapter of this R for Data Science guide. In this chapter, you've learned about:

*   **Creating R Packages:**  Structuring R packages, using `devtools` to create, document, build, install, and check packages, and options for sharing packages.
*   **Reproducible Research with R Markdown:**  Creating dynamic reports with R Markdown, combining text, code, and output, rendering documents, and key R Markdown features.
*   **Introduction to Deploying R Applications:**  Overview of Shiny app deployment options (shinyapps.io, Shiny Server, RStudio Connect), R APIs with Plumber, Docker containerization, and cloud deployment platforms.

With the skills and knowledge gained throughout this course, you are now well-equipped to embark on your journey as an R-powered data scientist. You can analyze data, create visualizations, build statistical and machine learning models, optimize your R code, and deploy your data science projects to share your work and insights with the world. Keep practicing, exploring, and building your data science expertise with R!
