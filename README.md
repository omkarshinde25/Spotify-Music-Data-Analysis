# Spotify Music Data Analysis — README

> **Project Summary:**  
> Interactive Power BI dashboard analyzing 27,800 Spotify songs from the *Top 50 Global* dataset.  
> This project demonstrates Power BI data modeling (star schema), Power Query transformations, KPI analysis, and interactive visuals using a dynamic slicer (Month & Quarter).  
> The report includes **four pages** — Overview, Artist Analysis, Songs Insights, and Album Analysis.

---

### Overview Page

<img src="https://github.com/omkarshinde25/Spotify-Music-Data-Analysis/blob/main/Dashboards/Spotify_Overview.png" width="800"> <br>

---

## Table of Contents

1. Project Overview  
2. Files & Images Included  
3. Data Model (Star Schema)  
4. Data Preparation & Transformations (Step-by-Step)  
5. Key Insights and KPIs  
6. Dashboard Pages & Visualisations (Detailed Point-by-Point)  
7. Navigation, Bookmarks & Buttons (Page Navigation Setup)  
8. Performance Recommendations  
9. How to Reproduce / Deliverables  
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

### Artist Analysis Page  
<img src="https://github.com/omkarshinde25/Spotify-Music-Data-Analysis/blob/main/Dashboards/Spotify_Artist.png" width="800"> <br>

### Songs Insights Page  
<img src="https://github.com/omkarshinde25/Spotify-Music-Data-Analysis/blob/main/Dashboards/Spotify_Songs.png" width="800"> <br>

### Album Analysis Page  
<img src="https://github.com/omkarshinde25/Spotify-Music-Data-Analysis/blob/main/Dashboards/Spotify_Album.png" width="800"> <br>

---

## 3. Data Model (Star Schema)

<img src="https://github.com/omkarshinde25/Spotify-Music-Data-Analysis/blob/main/Dashboards/Spotify_Star_Schema.png" width="800"> <br>

### Structure

* **Fact Table:** `Top-50-World` — song-level data with columns like Date, Position, Song, Artist, Popularity, Duration, Album Type, Total Tracks, Release Date, Explicit Flag, and Album Cover URL.  
* **Dimension Table:** `Slicer_Option` — supports dynamic switching between Month and Quarter.  
* **Measure Table:** stores calculated KPIs and metrics.

### Relationships

* `Top-50-World[Month]` linked with `Slicer_Option[Name]`.  
* Model follows a **Star Schema** design to optimize performance and simplify analysis.

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

### Album Analysis Page
* Album Type vs Total Songs chart  
* Explicit vs Non-Explicit song count per Album Type  
* Average Popularity per Album Type  

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
* Dashboard images: Overview, Artist, Songs, Album  
* `README.md` (this document)

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

---

**Created by:** Omkar Shinde  
**Tools Used:** Power BI, Power Query, DAX, Excel  
**Dataset:** Spotify Top 50 Global (27,800 rows)  
**Location:** Kolhapur, India  
**Contact:** shindeomkar2508@gmail.com  
**LinkedIn:** [https://www.linkedin.com/in/omkar-shinde-64a479245](https://www.linkedin.com/in/omkar-shinde-64a479245)  
**GitHub:** [https://github.com/omkarshinde25](https://github.com/omkarshinde25)
