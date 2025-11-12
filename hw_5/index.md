---
layout: default
title: HW5 - Altair Visualizations
---

## HW5: Illinois Licenses Visualizations - FALL 2022

Here are the two plots I made for the Fall 2022 Illinois Licenses dataset.

### Plot 1: Top 15 Most Common License Types


<div id="vis1"></div>

**Write-Up for Plot 1**

* **Description:** This plot shows the 15 most common types of licenses in the dataset. I wanted to get a simple overview of what kind of data I was working with, and this seemed like a good starting point.

* **Design & Encodings:** I used a horizontal bar chart (`mark_bar()`) because it's really good for comparing a quantitative value (the count) across different categories (the license types). The horizontal layout (`y='License Type'`, `x='count'`) is much easier to read than a vertical one since the category names are so long. I also sorted the chart (`sort='-x'`) so the most common license is at the top, which makes it easier to read.

* **Color:** I didn't use a special color map. A specific color for each bar wasn't necessary because the labels on the y-axis already tell you what each bar is. Using the single default color made the plot cleaner.

* **Transformations:** I had to do a few transformations in pandas to get the data ready. The original data has one row for every license, so I used `.value_counts()` to count how many times each `License Type` appeared. This list was huge, so I used `.nlargest(15)` to filter it down to just the top 15. Then I had to `.reset_index()` to turn it back into a DataFrame that Altair could read.

### Plot 2: Interactive Histogram of Licenses Issued Per Year

<!-- This div is where the second plot will be drawn -->

<div id="vis2"></div>

**Write-Up for Plot 2**

* **Description:** This plot is an interactive histogram that shows the number of licenses issued each year. The main feature is the dropdown menu that lets you filter this data by the "License Status."

* **Design & Encodings:** I used a vertical bar chart (`mark_bar()`) for this histogram. The **x-axis** is the `Year` (which I treated as ordinal data, `:O`), and the **y-axis** is the `count` of licenses issued (quantitative data).

* **Transformations:** 

  1. First, I had to convert the `Original Issue Date` column from a string to a real datetime object using `pd.to_datetime()`.

  2. Then, I created a new `Year` column by extracting the year from that date.

  3. When I first tried to plot, I got the `MaxRowsError`. To fix this , I used `alt.data_transformers.disable_max_rows()`.

* **Interactivity:** The interactivity is the dropdown menu. I created this using `alt.selection_point()` and bound it to a `binding_select()` with all the `License Status` options. This selection is then used to filter the chart with `.transform_filter()`. I think this really helps make the chart more useful. 
## Links

* **The Data:** [Link to the `licenses_fall2022.csv` file](https://github.com/UIUC-iSchool-DataViz/is445_data/raw/main/licenses_fall2022.csv)

* **The Analysis:** [Link to my Notebook](https://github.com/saibilla21/saibilla21.github.io/hw5/homework5.ipynb)

## Acknowledgements

I'd like to acknowledge that I used Gemini to help resolve Python syntax errors and debug Altair-related issues (like the `MaxRowsError`), and also for GitHub-related queries.

<!-- These are the scripts that make the plots work -->
<script src="https://cdn.jsdelivr.net/npm/vega@5"></script>

<script src="https://cdn.jsdelivr.net/npm/vega-lite@5"></script>

<script src="https://cdn.jsdelivr.net/npm/vega-embed@6"></script>

<script>
// Embed Plot 1
vegaEmbed('#vis1', 'plot1.json');

// Embed Plot 2
vegaEmbed('#vis2', 'plot2.json');
</script>
