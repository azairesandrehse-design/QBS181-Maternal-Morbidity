
# Geographic Differences in Maternal Characteristics, Prenatal Care, and Birth Outcomes in the United States (2024)

**QBS 181 — Data Wrangling | Cumulative Group Project**  
**Dartmouth College | Fall 2026**  
**Group Name:** Maternal Morbidity  
**Instructor:** Dr. Carly Bobak

## Project Team

| Name | Dartmouth Email |
|---|---|
| Azaire Andre | azaire.s.andre.hse@dartmouth.edu |
| Chuhan Wu (Hellarine) | chuhan.wu.gr@dartmouth.edu |
| Huiqian Xie | huiqian.xie.hse@dartmouth.edu |
| I-Chen Chen | i-chen.chen.hse@dartmouth.edu |

## 1. Project Overview

This project examines geographic differences in maternal characteristics, prenatal care utilization, and birth outcomes across U.S. counties in 2024.

Using natality data from the Centers for Disease Control and Prevention (CDC) and Rural-Urban Continuum Codes from the U.S. Department of Agriculture (USDA), we investigate how maternal characteristics and birth outcomes vary geographically and how average prenatal care utilization relates to county-level birth outcomes.

Our analysis focuses on county-level differences rather than individual-level outcomes. The project emphasizes data cleaning, data integration, transformation, exploratory data analysis, and reproducible workflows using R.

## 2. Research Questions and Objectives

### Aim 1: Geographic Differences in Maternal Characteristics and Birth Outcomes

Describe differences in maternal characteristics and birth outcomes across U.S. counties.

- Compare average maternal age, prepregnancy BMI, birth weight, and gestational age across the four U.S. Census regions.
- Identify counties with relatively high or low average birth weight and gestational age.
- Explore whether these geographic differences vary by metropolitan status.

### Aim 2: Prenatal Care Utilization and Birth Outcomes

Explore county-level relationships between average prenatal visits, maternal characteristics, and birth outcomes.

- Examine relationships between average prenatal visits and average birth weight and gestational age using scatterplots.
- Compare patterns across Census regions.
- Divide counties into lower, middle, and upper thirds based on average prenatal visits.
- Compare maternal characteristics and birth outcomes across these groups.
- Explore whether prenatal care relationships differ by region and metropolitan status.

## 3. Data Sources

### CDC WONDER Natality Data (2024)

**Source:** Centers for Disease Control and Prevention, National Center for Health Statistics.

Website: https://wonder.cdc.gov/

The dataset contains county-level natality information for U.S. live births occurring during 2024.

Variables include:

- Census region
- Census division
- State and county
- Geographic FIPS codes
- Number of births
- Average maternal age
- Average prepregnancy BMI
- Average birth weight
- Average obstetric-estimate gestational age
- Average number of prenatal visits

The original dataset contains 627 county-related observations: 578 individually identified counties and 49 groups of unidentified counties.

Unidentified county groups combine smaller counties and cannot be treated as individual counties when linking geographic classifications.

### USDA Rural-Urban Continuum Codes (2023)

**Source:** U.S. Department of Agriculture, Economic Research Service.

Website: https://www.ers.usda.gov/data-products/rural-urban-continuum-codes/

The USDA Rural-Urban Continuum Codes classify counties according to metropolitan status, population size, and proximity to metropolitan areas.

For this project:

- RUCC codes 1–3 are classified as metropolitan.
- RUCC codes 4–9 are classified as nonmetropolitan.

The RUCC dataset was merged with the CDC dataset using standardized county FIPS codes.

The 2023 RUCC classification provides geographic context for the 2024 natality outcomes.

## 4. Repository Contents

### R Code and Reports

- `Final_project_11.11.26_hw.Rmd` — Main R Markdown file containing data preparation, transformations, analyses, and visualizations.
- `Final_project_11.11.26_hw.html` — Rendered HTML report.

### Original and Processed Data

- `raw dataset_10.02.26_hw.xlsx` — Original CDC WONDER dataset.
- `cleaned_data_10.29.26.xlsx` — Cleaned CDC dataset used for analysis.
- `Ruralurbancontinuumcodes2023.xlsx` — USDA rural-urban classification data.
- `analysis_data_2024_rucc2023.rds` — Analysis-ready dataset following data integration.
- `aim1_results.rds` — Saved Aim 1 analysis results.
- `aim2_results.rds` — Saved Aim 2 analysis results.

### Summary Tables

The CSV files contain regional summaries, rurality comparisons, percentile cutoffs, prenatal visit group classifications, and outcome summaries.

Examples include:

- `regional_summary.csv`
- `regional_weighted_summary.csv`
- `rurality_summary.csv`
- `rurality_weighted_summary.csv`
- `rurality_by_region.csv`
- `percentile_cutoffs.csv`
- `prenatal_cutoffs.csv`
- `prenatal_group_summary.csv`
- `prenatal_group_check.csv`
- `region_group_summary.csv`

Additional CSV files contain group counts and detailed results.

### Visualizations

The PNG files contain generated figures for both research aims.

Examples include:

- `county_maps.png`
- `regional_boxplots.png`
- `rurality_boxplots.png`
- `overall_scatter.png`
- `regional_scatter.png`
- `rurality_scatter.png`
- `prenatal_group_boxplots.png`
- `regional_group_boxplots.png`

### Project Proposal

- `data approval.docx` — Project background, approved research aims, data description, and references.

## 5. Data Cleaning and Wrangling Process

The data-wrangling pipeline was designed to prepare the CDC and USDA datasets for geographic comparisons and exploratory analyses.

### Step 1: Data Acquisition

The group obtained 2024 natality data from CDC WONDER and the 2023 Rural-Urban Continuum Codes from USDA.

The original datasets were retained to preserve the source information.

### Step 2: Preliminary Data Cleaning

Preliminary cleaning was conducted in Excel.

The CDC export included county observations alongside higher-level geographic summary rows. A cleaned county-level workbook was prepared for analysis.

The original and cleaned workbooks are both included in this repository.

The R Markdown analysis begins with the cleaned workbook. The complete sequence of preliminary Excel operations is not contained in the R Markdown file.

### Step 3: Importing and Formatting Data in R

The cleaned CDC and USDA datasets were imported into R using the `readxl` package.

Variables were converted to appropriate data types, including numeric measurements and categorical geographic classifications.

Geographic identifiers were formatted to support consistent matching between datasets.

### Step 4: Geographic Identifier Standardization

County FIPS codes were standardized to five-character identifiers.

State FIPS codes were standardized to two characters.

Leading zeros were preserved to prevent incorrect county matching.

The code also includes validation checks and a correction for the recorded Benton County, Arkansas FIPS identifier.

### Step 5: Identifying Eligible Counties

Pooled unidentified county records were distinguished from individually identified counties.

These pooled records were excluded from analyses requiring individual county identification, geographic mapping, or a one-to-one RUCC match.

The main county-level analyses use 578 individually identified counties.

### Step 6: Merging CDC and USDA Data

A relational left join was performed using county FIPS codes.

The join added rural-urban classification information to the CDC natality observations.

The analysis includes checks for unmatched geographic identifiers and missing classification values.

Among the individually identified counties:

- 550 were classified as metropolitan.
- 20 were classified as nonmetropolitan.
- 8 Connecticut counties did not have matching RUCC classifications.

Counties without RUCC classifications were excluded from metropolitan-status comparisons but retained where RUCC information was not required.

### Step 7: Data Validation

The integrated dataset was examined for:

- Missing values
- Unmatched geographic identifiers
- Duplicate or inconsistent geographic codes
- Observation counts
- Appropriate numeric and categorical variable formats

These checks helped establish which observations could be used in each analysis.

## 6. Aim 1: Geographic Analysis

### Regional Comparisons

County-level distributions of maternal age, prepregnancy BMI, birth weight, and gestational age were compared across the Northeast, Midwest, South, and West.

Boxplots and descriptive summary tables were used to examine geographic differences.

Each county received equal weight in the primary plots. Additional summaries weighted by the number of births were produced for comparison.

### Identifying High and Low Counties

The 10th and 90th percentiles of county-average birth weight and gestational age were used to identify relatively low and high counties.

Geographic maps were created to visualize the locations of these counties.

### Rural-Urban Comparisons

Counties were grouped by metropolitan status using the RUCC classification.

Boxplots and summary statistics were used to explore differences in maternal characteristics and birth outcomes between metropolitan and nonmetropolitan counties.

## 7. Aim 2: Prenatal Visits and Birth Outcomes

### Scatterplot Analysis

Scatterplots were used to examine associations between:

- Average prenatal visits and average birth weight
- Average prenatal visits and average gestational age

Analyses were conducted overall and separately by Census region and metropolitan classification.

### Prenatal Visit Group Classification

Counties were divided into three approximately equal-sized groups based on average prenatal visits:

- Lower third: 193 counties
- Middle third: 192 counties
- Upper third: 193 counties

The same overall group cutoffs were used across Census regions.

### Group Comparisons

Boxplots and summary tables compared maternal age, prepregnancy BMI, birth weight, and gestational age across prenatal-visit groups.

Additional comparisons examined the patterns within each Census region.

## 8. Reproducing the Analysis

### Required Software

- R (version 4.x recommended)
- RStudio (recommended)
- R Markdown

The analysis uses the following R packages:

- `readxl`
- `dplyr`
- `stringr`
- `tidyr`
- `ggplot2`
- `tigris`
- `sf`
- `rmarkdown`
- `knitr`

Install these packages using:

```r
install.packages(c(
  "readxl", "dplyr", "stringr", "tidyr",
  "ggplot2", "tigris", "sf",
  "rmarkdown", "knitr"
))
```

### Running the Project

1. Download or clone this GitHub repository.
2. Open RStudio and set the working directory to the downloaded project folder.
3. Open `Final_project_11.11.26_hw.Rmd`.
4. Install any required packages that are not already installed.
5. Update the original computer-specific file paths in a working copy of the R Markdown file.

The CDC and USDA input file references should point to:

```r
"cleaned_data_10.29.26.xlsx"
"Ruralurbancontinuumcodes2023.xlsx"
```

Use the worksheet names `county level data` and `Rural-urban Continuum Code 2023`, respectively.

The paths used to save results should also point to accessible locations within the project directory.

To regenerate the merged analysis dataset, the working copy should include the following operation after creating `analysis_data`:

```r
saveRDS(analysis_data, "analysis_data_2024_rucc2023.rds")
```

6. Run or knit the R Markdown analysis using RStudio.
7. Review the resulting HTML report, figures, summary tables, and saved R objects.
8. Compare newly generated results with the output files included in this repository.

For example, once paths have been adjusted, the R Markdown file can be rendered using:

```r
rmarkdown::render("Final_project_11.11.26_hw.Rmd")
```

The county mapping steps may require internet access to retrieve geographic boundary data through `tigris`.

**Reproducibility note:** The original R Markdown contains local file paths and begins with the previously cleaned Excel workbook. Reproducing the complete process from the raw CDC export requires the preliminary Excel cleaning steps to be documented or implemented separately. A full end-to-end rerun on a fresh computer has not yet been verified.

## 9. Main Findings

The analysis identified geographic differences in county-average maternal characteristics, prenatal care utilization, and birth outcomes.

### Geographic Differences

County-average birth weight and gestational age varied across U.S. Census regions.

The South generally had lower county-average birth weight and gestational age than several other regions.

### Prenatal Care Utilization

Counties with fewer average prenatal visits generally had lower average birth weights than counties in the middle and upper prenatal-visit groups.

However, substantial overlap existed across groups.

### Regional Patterns

Associations between prenatal visits and birth outcomes varied across Census regions.

The analyses also showed differences in maternal characteristics and prenatal care patterns across geographic areas.

### Metropolitan Status

Metropolitan and nonmetropolitan comparisons showed variation in county-average outcomes.

However, the small number of individually identified nonmetropolitan counties limits the generalizability of these findings.

These results describe county-level associations rather than causal effects.

## 10. Study Limitations

Several limitations should be considered when interpreting the results.

**County-level data:** The analysis uses aggregated county averages rather than individual maternal or infant records. Individual-level conclusions cannot be drawn from these results.

**Limited rural representation:** Smaller counties were grouped in the original CDC dataset, and many could not be individually classified or mapped.

**Unequal county populations:** Counties vary substantially in the number of births. Primary visualizations weight counties equally, although birth-weighted summaries are also available.

**Prenatal visits and pregnancy duration:** Shorter pregnancies allow fewer opportunities for prenatal visits, which may partly explain associations between prenatal visit counts and gestational age.

**Unmeasured factors:** Income, education, insurance coverage, health care access, and other maternal or community characteristics may influence the observed relationships.

## 11. Future Research

Potential extensions include:

- Integrating county-level socioeconomic measures from the American Community Survey.
- Adding health care access indicators from HRSA or County Health Rankings.
- Examining additional rural-urban classification categories.
- Assessing whether geographic associations remain after accounting for potential confounders.
- Incorporating preterm birth rates or other outcomes when appropriate data are available.

These extensions could provide additional context for understanding geographic differences in maternal and infant health.

## 12. AI-Use Disclosure

ChatGPT (OpenAI) was used to draft and organize this README. All other project work, including data preparation, coding, analyses, figures, and results, was completed independently by the group.

## 13. References

1. Centers for Disease Control and Prevention. CDC WONDER Natality Database. https://wonder.cdc.gov/

2. U.S. Department of Agriculture, Economic Research Service. Rural-Urban Continuum Codes. https://www.ers.usda.gov/data-products/rural-urban-continuum-codes/

3. National Center for Health Statistics. U.S. Births Increase by 1% in 2024. CDC, 2025.

4. March of Dimes. 2024 March of Dimes Report Card.

5. Driscoll AK, Gregory ECW. Increases in Prepregnancy Obesity: United States, 2016–2019. NCHS Data Brief No. 392, 2020.

Additional references and original project background are provided in `data approval.docx`.

---

**QBS 181 — Data Wrangling**  
**Dartmouth College | Fall 2026**  
**Maternal Morbidity Group**
