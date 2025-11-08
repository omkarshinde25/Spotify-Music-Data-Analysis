# Spotify Music Data Analysis — README

> **Project Summary:**  
> Interactive Power BI dashboard analyzing 27,800 Spotify songs from the *Top 50 Global* dataset.  
> This project demonstrates Power BI data modeling , Power Query transformations, KPI analysis, and interactive visuals using a dynamic slicer (Month & Quarter).  
> The report includes **four pages** — Home, Overview, Artist Analysis, Songs Insights.

---

### Overview Page

<img src="https://github.com/omkarshinde25/Spotify-Music-Data-Analysis/blob/main/Dashboard%20PNG/Overview%20Page.png" width="800"> <br>

---

## Table of Contents

1. Project Overview  
2. Files & Images Included  
3. Data Modeling 
4. Data Preparation & Transformations (Step-by-Step)  
5. Key Insights and KPIs  
6. Dashboard Pages & Visualisations (Detailed Point-by-Point)  
7. Navigation, Bookmarks & Buttons (Page Navigation Setup)  
8. Performance Recommendations  
9. How to Reproduce
10. Project Outcome

---

## 1. Project Overview

This Power BI project analyzes **Spotify Top 50 Global data (27,800 rows)** containing key attributes such as song name, artist, popularity, duration, album type, total tracks, release date, and explicit flag.

### Business Goals:
* Track total songs, distinct artists, average popularity, and average duration KPIs.  
* Compare **explicit vs non-explicit** songs.  
* Analyze **album types** (Single, Album, Compilation).  
* Identify **top artists** and **top songs** based on popularity.  
* Enable dynamic analysis through **Month/Quarter slicer** for time-based insights.

**Audience:** Spotify analytics team, playlist curators, and marketing strategists.

---

## 2. Files & Images Included

* `Top-50-World.csv` — main fact table (27,800 rows)  
* `Dynamic Slicer Table` — used for Month/Quarter switching  
* `Measure Table` — centralized table for all KPIs  

Dashboard Screenshots (for visual preview):

### Home Page
<img src="https://github.com/omkarshinde25/Spotify-Music-Data-Analysis/blob/main/Dashboard%20PNG/Home%20Page.png" width="800"> <br>

### Overview Page
<img src="https://github.com/omkarshinde25/Spotify-Music-Data-Analysis/blob/main/Dashboard%20PNG/Overview%20Page.png" width="800"> <br>

### Artist Analysis Page  
<img src="https://github.com/omkarshinde25/Spotify-Music-Data-Analysis/blob/main/Dashboard%20PNG/Artists%20Page.png" width="800"> <br>

### Songs Insights Page  
<img src="https://github.com/omkarshinde25/Spotify-Music-Data-Analysis/blob/main/Dashboard%20PNG/Songs%20Page.png" width="800"> <br>


---

## 3. Data Modeling

<img src="https://github.com/omkarshinde25/Spotify-Music-Data-Analysis/blob/main/Dashboard%20PNG/Schema.png" width="800"> <br>

### Structure

* **Fact Table:** `Top-50-World` — song-level data with columns like Date, Position, Song, Artist, Popularity, Duration, Album Type, Total Tracks, Release Date, Explicit Flag, and Album Cover URL.  
* **Dimension Table:** `Slicer_Option` — supports dynamic switching between Month and Quarter.  
* **Measure Table:** stores calculated KPIs and metrics.


---

## 4. Data Preparation & Transformations (Step-by-Step)

Performed in **Power Query** within Power BI:

1. Imported the `Top-50-World.csv` file.  
2. Changed data types:  
   * Date → Date  
   * Popularity → Whole Number  
   * Duration → Converted from milliseconds to minutes  
3. Added new calculated columns for Month, Quarter, and Year.  
4. Cleaned text fields — trimmed spaces and capitalized artist names.  
5. Removed duplicates and blank rows.  
6. Normalized the `is_explicit` column to True/False values.  
7. Loaded cleaned tables into Power BI and created relationships in Model View.

---

## 5. Key Insights and KPIs

* **Total Songs:** Total number of unique songs in the dataset.  
* **Distinct Artists:** Total number of unique artists featured.  
* **Average Popularity:** Mean popularity score of all songs.  
* **Average Duration:** Average song length in minutes.  
* **Explicit vs Non-Explicit:** Comparison of songs marked explicit vs non-explicit.  
* **Popularity by Month:** Trend analysis of overall popularity across time periods.

### Dynamic Slicer Measure 

```dax
Slicer_Option = {
    ("Month", NAMEOF('Top-50-World'[Month]), 0),
    ("Quarter", NAMEOF('Top-50-World'[Qtr]), 1)
}
```
## Measure Overview, Artists, Songs

```dax
DEFINE
    MEASURE 'Top-50-world'[Total Songs] = COUNTROWS('Top-50-world')
    MEASURE 'Top-50-world'[Distinct Songs] = DISTINCTCOUNT('Top-50-world'[song])
    MEASURE 'Top-50-world'[Distinct Artists] = DISTINCTCOUNT('Top-50-world'[artist])
    MEASURE 'Top-50-world'[Avg Popularity] = AVERAGE('Top-50-world'[popularity])
    MEASURE 'Top-50-world'[Max Popularity] = MAX('Top-50-world'[popularity])
    MEASURE 'Top-50-world'[Min Popularity] = MIN('Top-50-world'[popularity])

    MEASURE 'Top-50-world'[Avg Duration Minutes] = AVERAGE('Top-50-world'[duration_ms]) / 60000
    MEASURE 'Top-50-world'[Max Duration Minutes] = MAX('Top-50-world'[duration_ms]) / 60000
    MEASURE 'Top-50-world'[Min Duration Minutes] = MIN('Top-50-world'[duration_ms]) / 60000

    MEASURE 'Top-50-world'[Explicit Songs] = CALCULATE(COUNTROWS('Top-50-world'), 'Top-50-world'[is_explicit] = TRUE())
    MEASURE 'Top-50-world'[Non-Explicit Songs] = CALCULATE(COUNTROWS('Top-50-world'), 'Top-50-world'[is_explicit] = FALSE())
    MEASURE 'Top-50-world'[Pct Explicit Songs] = DIVIDE([Explicit Songs], [Total Songs], 0)
    MEASURE 'Top-50-world'[Avg Popularity Explicit] = CALCULATE(AVERAGE('Top-50-world'[popularity]), 'Top-50-world'[is_explicit] = TRUE())
    MEASURE 'Top-50-world'[Avg Popularity NonExplicit] = CALCULATE(AVERAGE('Top-50-world'[popularity]), 'Top-50-world'[is_explicit] = FALSE())

    MEASURE 'Top-50-world'[Avg Position] = AVERAGE('Top-50-world'[position])
    MEASURE 'Top-50-world'[Position 1 Songs] = CALCULATE(COUNTROWS('Top-50-world'), 'Top-50-world'[position] = 1)
    MEASURE 'Top-50-world'[Position 1 Artists] = CALCULATE(DISTINCTCOUNT('Top-50-world'[artist]), 'Top-50-world'[position] = 1)

    MEASURE 'Top-50-world'[Avg Tracks per Album] = AVERAGE('Top-50-world'[total_tracks])
    MEASURE 'Top-50-world'[Album Type Count] = DISTINCTCOUNT('Top-50-world'[album_type])
    MEASURE 'Top-50-world'[Singles Count] = CALCULATE(COUNTROWS('Top-50-world'), 'Top-50-world'[album_type] = "single")
    MEASURE 'Top-50-world'[Albums Count] = CALCULATE(COUNTROWS('Top-50-world'), 'Top-50-world'[album_type] = "album")

    -- Artist-scoped (use when Artist in context)
    MEASURE 'Top-50-world'[Songs per Artist] = COUNTROWS('Top-50-world')
    MEASURE 'Top-50-world'[Distinct Songs per Artist] = DISTINCTCOUNT('Top-50-world'[song])
    MEASURE 'Top-50-world'[Avg Popularity per Artist] = AVERAGE('Top-50-world'[popularity])
    MEASURE 'Top-50-world'[Position1 Hits per Artist] = CALCULATE(COUNTROWS('Top-50-world'), 'Top-50-world'[position] = 1)

    -- Time-scoped (use when Year in context)
    MEASURE 'Top-50-world'[Songs per Year] = COUNTROWS('Top-50-world')
    MEASURE 'Top-50-world'[Avg Popularity per Year] = AVERAGE('Top-50-world'[popularity])
    MEASURE 'Top-50-world'[Avg Duration per Year] = AVERAGE('Top-50-world'[duration_ms]) / 60000
    MEASURE 'Top-50-world'[Pct Explicit per Year] = DIVIDE(
        CALCULATE(COUNTROWS('Top-50-world'), 'Top-50-world'[is_explicit] = TRUE()),
        [Songs per Year], 
        0
    )

EVALUATE
    SUMMARIZECOLUMNS(
        "Total Songs", [Total Songs],
        "Distinct Songs", [Distinct Songs],
        "Distinct Artists", [Distinct Artists],
        "Avg Popularity", [Avg Popularity],
        "Max Popularity", [Max Popularity],
        "Min Popularity", [Min Popularity],
        "Avg Duration Minutes", [Avg Duration Minutes],
        "Max Duration Minutes", [Max Duration Minutes],
        "Min Duration Minutes", [Min Duration Minutes],
        "Explicit Songs", [Explicit Songs],
        "Non-Explicit Songs", [Non-Explicit Songs],
        "Pct Explicit Songs", [Pct Explicit Songs],
        "Avg Popularity Explicit", [Avg Popularity Explicit],
        "Avg Popularity NonExplicit", [Avg Popularity NonExplicit],
        "Avg Position", [Avg Position],
        "Position 1 Songs", [Position 1 Songs],
        "Position 1 Artists", [Position 1 Artists],
        "Avg Tracks per Album", [Avg Tracks per Album],
        "Album Type Count", [Album Type Count],
        "Singles Count", [Singles Count],
        "Albums Count", [Albums Count],
        "Songs per Artist", [Songs per Artist],
        "Distinct Songs per Artist", [Distinct Songs per Artist],
        "Avg Popularity per Artist", [Avg Popularity per Artist],
        "Position1 Hits per Artist", [Position1 Hits per Artist],
        "Songs per Year", [Songs per Year],
        "Avg Popularity per Year", [Avg Popularity per Year],
        "Avg Duration per Year", [Avg Duration per Year],
        "Pct Explicit per Year", [Pct Explicit per Year]
    )

```


---

## 6. Dashboard Pages & Visualisations (Detailed Point-by-Point)

### Overview Page
* Key KPIs: Total Songs, Distinct Artists, Avg Popularity, Avg Duration  
* Donut Charts: Explicit vs Non-Explicit, Album Type Distribution  
* Bar Chart: Popularity by Month  
* Line Chart: Average Popularity by Year  
* Top Songs & Top Artists Cards

---

### Artist Analysis Page
* Top 10 Artists by Popularity  
* Songs per Artist visualization  
* Total Tracks per Artist analysis  
* Average Popularity comparison by Artist  

---

### Songs Insights Page
* Top 10 Songs ranked by Popularity  
* Songs grouped by Album Type  
* Table visual with Song, Artist, Duration, Release Date, and Popularity  

---

## 7. Navigation, Bookmarks & Buttons (Page Navigation Setup)

**Steps to set up interactive navigation:**

1. Import PNG icons for each page (Home, Artist, Songs, Album).  
2. Create a **Bookmark** for each page (View → Bookmarks Pane).  
3. Select the image → Enable **Action** → Set **Type** to Bookmark → Link to the target page.  
4. Repeat for all navigation icons and align them consistently on all pages.  
5. Add a **Back button** to return to the Overview page.

---

## 8. Performance Recommendations

* Use **Import mode** for efficient processing (dataset < 30k rows).  
* Remove unused columns (e.g., `album_cover_url` if not displayed).  
* Replace long text columns with keys if used repeatedly.  
* Use **measures** instead of calculated columns for better performance.  
* Avoid visuals that process more than 10,000 data points simultaneously.  
* Maintain consistent formatting and minimal visuals per page for clarity.

---

## 9. How to Reproduce / Deliverables

### Files Delivered
* Power BI `.pbix` file  
* Cleaned dataset: `Top-50-World.csv`  
* Dashboard PNG: Overview, Artist, Songs, Album  
* `README.md` 

### Steps to Reproduce
1. Open Power BI Desktop → Load `Top-50-World.csv`.  
2. Apply Power Query transformations and calculated columns.  
3. Create visuals as described above.  
4. Add slicers, cards, charts, and bookmarks.  
5. Configure page navigation using images and bookmarks.  
6. Export `.pbix` and dashboard screenshots for documentation.  

---

## 10. Project Outcome

This Power BI dashboard provides an interactive view of **Spotify music performance metrics**, focusing on song popularity, artist success, and album-type distribution.  

**Key outcomes:**
* Clear understanding of top-performing artists and songs.  
* Insight into content type distribution (Albums, Singles, Compilations).  
* Visualization of monthly and yearly popularity trends.  
* Efficient navigation and dynamic insights via slicers and bookmarks.  

