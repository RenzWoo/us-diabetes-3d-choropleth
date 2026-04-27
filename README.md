# U.S. Diabetes 3D Choropleth Map

> A 3D rayshader visualization of adult diabetes prevalence across all contiguous U.S. counties using CDC data.

**Authors:** RenzWoo &nbsp;|&nbsp; **Date:** 2025  
**Data:** CDC Diabetes Atlas 2021

![Map](3D-population_A3.png)

---

## Objective

This project visualizes the geographic distribution of adult diabetes prevalence (ages 20+) across every county in the contiguous United States. Rather than a flat choropleth, we used `rayshader` to extrude each county by its prevalence value — turning the map into a 3D landscape where height and color both encode diabetes rates. This dual encoding makes regional clusters immediately readable, particularly the concentration of high-prevalence counties across the Southeast U.S.

---

## Key Findings

1. **Median prevalence is 8.3%** across contiguous U.S. counties, but the distribution is highly uneven.

2. **Highest prevalence counties peak at 17.9%** — Todd County leads, followed by Williamsburg County (17.5%), Portsmouth City (16.8%), Holmes County (15.5%), and Gadsden County (15.9%). These are heavily concentrated in the South.

3. **Case count and prevalence are weakly correlated (r = 0.12).** High raw case counts tend to appear in densely populated urban counties, while high *prevalence rates* cluster in rural Southern counties — two distinct patterns that a flat count map would obscure.

---

## Dataset

| Source | File |
|--------|------|
| [CDC Diabetes Atlas 2021](https://www.cdc.gov/diabetes/data/) | `Complete_Merged_DiabetesAtlas_CountyData.csv` |
| U.S. Census TIGER/Line — County Boundaries | `National Sub-State Geography.gpkg` |

> **Note:** The `.gpkg` boundary file may exceed GitHub's 100MB limit. If so, download it directly from the [U.S. Census Bureau TIGER/Line files](https://www.census.gov/geographies/mapping-files/time-series/geo/tiger-line-file.html) and place it in the `data/` folder before running.

---

## Tech Stack

- **Language:** R
- **3D rendering:** `rayshader`
- **Spatial data:** `sf`, `stars`, `raster`
- **Visualization:** `ggplot2`, `MetBrewer` (Isfahan1 palette)
- **Data wrangling:** `dplyr`, `stringr`, `readr`

---

## How to Run

```bash
# 1. Clone the repository
git clone https://github.com/your-username/us-diabetes-3d-choropleth.git
cd us-diabetes-3d-choropleth
```

```r
# 2. Install required R packages (run once in R or RStudio)
install.packages(c("sf", "dplyr", "ggplot2", "readr", "stringr",
                   "raster", "stars", "rayshader", "MetBrewer", "gridExtra"))
```

3. Place the data files in the `data/` folder (see Dataset section above).
4. Open `3D_choropleth_US.Rmd` in RStudio.
5. Click **Knit → Knit to PDF** to run the full pipeline.

> ⚠️ **Render time warning:** The final `render_highquality()` step runs at 2400×3000px with 300 samples and parallel rendering enabled. Expect **30–90 minutes** depending on your CPU/RAM. The intermediate 2D map and 3D preview will render much faster.

---

## Folder Structure

```
us-diabetes-3d-choropleth/
├── README.md
├── 3D_choropleth_US.Rmd
├── 3D-population_A3.png            ← poster visual
├── data/
│   ├── Complete_Merged_DiabetesAtlas_CountyData.csv
│   └── National Sub-State Geography.gpkg
└── outputs/
    └── USA_diabetes_3d_map.png     ← high-res render output
```

---

## .gitignore

Add the following to avoid committing large temp files:

```
*.rgl
*.rds
*.RData
.Rhistory
.Rproj.user/
outputs/USA_diabetes_3d_map.png
```

> The high-res render output (`USA_diabetes_3d_map.png`) is excluded by default due to file size. The poster (`3D-population_A3.png`) is committed directly to the root for README display.
