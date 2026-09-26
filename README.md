# Youth Development & Economic Opportunity Analytics

## Project Overview

This project analyzes the relationship between economic conditions, education completion, youth unemployment, and youth disengagement (NEET) across countries and over time.

The analysis combines internationally comparable indicators from the World Bank and International Labour Organization (ILO/ILOSTAT) and presents the results through exploratory data analysis and an interactive Power BI dashboard.

## Research Questions

- How does GDP per capita relate to lower-secondary completion?
- How is NEET prevalence related to youth unemployment?
- How do youth unemployment and NEET rates change over time?
- Which countries have the highest GDP per capita and NEET rates within the analytical dataset?
- Which countries have the lowest lower-secondary completion rates?
- How do the four indicators vary for an individual selected country?

## Indicators

| Indicator | Source | Unit |
|---|---|---|
| GDP per capita, PPP (constant 2021 international $) | World Bank | International dollars |
| Lower-secondary completion rate | World Bank | % |
| Youth unemployment | ILO/ILOSTAT | % |
| NEET rate | ILO/ILOSTAT | % |

## Data Preparation

The source datasets were prepared and aligned using country-year keys.

Main preparation steps included:

- Selecting the required fields from the World Bank and ILO datasets.
- Standardizing country, country-code, and year fields.
- Converting the youth unemployment dataset from wide to long format.
- Filtering the NEET dataset to the `Total` sex category.
- Checking for duplicate country-year observations.
- Identifying countries and years common to all four datasets.
- Excluding aggregate geographic entities such as `World` and `Sub-Saharan Africa` from the country-level analytical dataset.
- Merging the four indicators using country and year.
- Removing the single analytical observation with a missing NEET rate.
- Preserving source/status metadata for the NEET observations.

The final analytical dataset contains **1,256 country-year observations** across **121 countries**.

## Exploratory Data Analysis

The analysis included:

- Descriptive statistics
- Pearson correlation analysis
- Scatter-plot analysis
- Investigation of extreme observations
- Spearman rank correlation analysis
- GDP distribution analysis

### Correlation Analysis

Pearson and Spearman correlations were compared to examine both linear and monotonic relationships.

| Relationship | Pearson | Spearman |
|---|---:|---:|
| GDP ↔ Education Completion | +0.545 | +0.715 |
| GDP ↔ Youth Unemployment | -0.045 | +0.138 |
| GDP ↔ NEET | -0.628 | -0.705 |
| Education ↔ Youth Unemployment | +0.287 | +0.315 |
| Education ↔ NEET | -0.392 | -0.482 |
| Youth Unemployment ↔ NEET | +0.284 | +0.263 |

These correlations describe associations in the observed country-year data and should not be interpreted as evidence of causation.

## Important Data Considerations

Extreme values were investigated rather than automatically removed.

For example, the lower-secondary completion indicator can legitimately exceed 100% because of the methodology used for this World Bank indicator. High GDP per capita values and high youth unemployment or NEET observations were also retained unless there was evidence that an observation was erroneous or methodologically incompatible.

The NEET status field is treated as metadata rather than as a measurement. Status values such as `Break in series` and `Unreliable` are used to support interpretation and data-quality assessment.

## Power BI Dashboard

The final dashboard contains four pages:

### Page 1 — Global Youth Development Overview

Provides a high-level view of the dataset, including:

- Total countries
- Total observations
- Average GDP per capita
- Average NEET rate
- Indicator trends over time
- Country and year filters

### Page 2 — Economic Conditions & Education

Examines:

- GDP per capita vs lower-secondary completion
- Average GDP per capita by country
- Lowest 10 countries by average education completion

### Page 3 — Youth Disengagement: NEET

Examines:

- NEET rate vs youth unemployment
- Highest 10 countries by average NEET rate
- NEET rate over time

### Page 4 — Country & Youth Labour Market Explorer

Provides an interactive country-level view with:

- GDP per capita
- Education completion
- Youth unemployment
- NEET rate
- Youth unemployment and NEET trends
- Education completion trends
- GDP per capita trends

## Data Sources & Documentation

### World Bank

- GDP per capita, PPP (constant 2021 international $)
- Lower-secondary completion rate

Official documentation:

- https://data360files.worldbank.org/data360-data/metadata/WB_WDI_NY_GDP_PCAP_PP_KD.pdf
- https://databank.worldbank.org/metadataglossary/world-development-indicators/series/SE.SEC.CMPT.LO.FE.ZS

### International Labour Organization

Youth labour-market indicators were obtained from ILO/ILOSTAT.

Official resources:

- https://ilostat.ilo.org/data/
- https://ilostat.ilo.org/methods/
- https://ilostat.ilo.org/dataviz/weso/

## Tools Used

- Python
- Pandas
- Matplotlib
- Seaborn
- Power BI
- DAX
- Jupyter Notebook / Google Colab

## Limitations

- The final dataset represents the exact country-year intersection available across all four indicators after data preparation.
- Country coverage and time coverage vary between indicators.
- The observations are repeated country-year records, so simple correlations should not be interpreted as causal relationships.
- Some source observations contain methodological or comparability flags.
- Differences in indicator definitions and source methodologies should be considered when interpreting cross-country comparisons.

## Data Availability

The original raw source files are not included in the repository. They are available from the official World Bank and ILO/ILOSTAT sources linked above.

The repository can include the final cleaned analytical dataset because it is small and directly supports reproducibility, provided the underlying source-data redistribution terms allow it.

The notebook documents the transformation and merging steps used to produce the analytical dataset from the official source data.
