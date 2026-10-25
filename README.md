<div align="center">
  <img src="https://raw.githubusercontent.com/ryanconquers/climate-trends-and-paleoclimate-reconstruction/main/assets/climate-research-banner.png"
       alt="Climate Trends and Paleoclimate Reconstruction"
       width="100%">
</div>

# Global Temperature Analysis: Modern Observations and Paleoclimate Reconstruction

This project explores global temperature variability using recent instrumental-era observations and a long paleoclimate reconstruction. It examines modern temperature trends, reconstructed historical patterns, ensemble uncertainty, and agreement between the reconstruction and its instrumental target. The notebooks include saved outputs and narrative interpretation.

**Research affiliation:** Astitva  
**Role:** Scenario Analyst at Astitva

This identifies the research affiliation and role supplied by the researcher; it does not imply institutional endorsement or approval of the analysis.

## Research objectives

- Describe global annual temperature anomalies from 1940 to 2025 and compare trends across selected periods.
- Examine reconstructed global temperature variability from the PAGES2k Consortium's two-millennium reconstruction.
- Summarize the reconstruction's ensemble uncertainty and compare its median with the Cowtan and Way instrumental target during their shared years.
- Explore differences among India, China, and the United States in the modern anomaly dataset.

## Project files

| File | Purpose |
| --- | --- |
| `Climate_Variability_and_Environmental_Resilience_Finalized.ipynb` | Main analysis notebook, with saved outputs and written findings. |
| `Climate_Variability_and_Environmental_Resilience.ipynb` | Earlier version of the analysis, retained as a separate notebook. |
| `annual-temperature-anomalies.csv` | Annual temperature anomalies by entity, with columns `entity`, `code`, `year`, and `temperature_anomaly`. |
| `average-annual-surface-temperature.csv` | Annual average 2 m temperatures by entity, with columns `entity`, `code`, `year`, and `temperature_2m`. |
| `Full_ensemble_median_and_95pct_range.txt` | PAGES2k global mean temperature reconstruction ensemble summary and Cowtan and Way instrumental target, including annual and 31-year-filtered series. |

The two CSV files contain 213 entities each and cover 1940–2025. The PAGES2k text file contains Year CE, ensemble median and 2.5th/97.5th percentile estimates, and the instrumental target. Its header documents values as °C relative to 1961–1990 over an April–March annual average.

## Data sources and interpretation

The notebook identifies the modern temperature files as Our World in Data (OWID) data and uses the entity `World` for global results. The historical reconstruction file identifies its source as the PAGES2k Consortium 2019 global mean temperature reconstruction compilation; its instrumental target is identified as Cowtan and Way. The data files are included in this project so the analyses do not require a download step.

The project files do not provide direct source URLs, dataset release identifiers beyond those named in the notebook and data header, or a separate citation file. Consult the dataset headers and notebook context for the source descriptions above.

The modern anomaly values use the baseline and conventions of the OWID source. The historical reconstruction uses a 1961–1990 reference period and an April–March year. These series therefore do not share a common baseline or necessarily the same averaging conventions. The final combined visualization in the notebook centers each series on its own 1940–2000 mean to compare relative departures; it does not make the underlying records equivalent.

## Methodology

The notebooks load the two CSV datasets with pandas, inspect their dimensions and coverage, and select global or country records by entity. They plot annual series, compute endpoint differences and decade or period averages, and estimate linear trends. The finalized notebook also:

- Compares 1940–1979 and 1980–2025 modern trends, including an interaction regression with heteroskedasticity-and-autocorrelation-consistent (HAC) standard errors and a sensitivity check across HAC lag choices.
- Searches candidate years for an exploratory two-segment fit and compares its fit with a single linear trend.
- Reads the PAGES2k tab-separated file, plots its median and ensemble interval, and examines the provided 31-year-filtered series.
- Compares the PAGES2k reconstruction median with the Cowtan and Way instrumental target over their overlap using MAE, RMSE, correlation, and residual summaries.
- Summarizes reconstructed anomalies over selected historical periods and explores how the ensemble interval width changes through time.

## Key findings

The values below are reported by the finalized notebook and are descriptive results from the supplied data and selected analysis choices.

- The global modern anomaly changes from −0.686 °C in 1940 to +0.592 °C in 2025, a difference of +1.278 °C. The fitted linear trend for 1940–2025 is +0.142 °C per decade (R² = 0.8261).
- The estimated trend is about +0.018 °C per decade for 1940–1979 and +0.213 °C per decade for 1980–2025. HAC inference and the lag sensitivity analysis support a steeper fitted trend in the later period under the tested specifications.
- The exploratory two-segment search selects 1976 as its best-fitting candidate breakpoint. Nearby candidate years fit similarly, so this is not an exact physical turning point.
- The historical reconstruction shows variability across the approximately two-millennium record, with cooler reconstructed anomalies during portions of the second millennium and an increase near the end of its record. The ensemble interval is generally wider in earlier portions of this dataset, though its width varies over time.
- Over 1850–2000, the reconstruction median and instrumental target have MAE 0.059 °C, RMSE 0.075 °C, and Pearson correlation 0.944. The mean residual is −0.0029 °C (reconstruction minus target). This is agreement over their overlap, not independent validation.
- Mean reconstructed anomalies increase across the notebook's selected periods: −0.3820 °C (1850–1899), −0.2163 °C (1900–1949), −0.0442 °C (1950–1979), and +0.1829 °C (1980–2000). The first-to-last difference is +0.5649 °C between period means.
- In the country comparison, estimated anomaly trends are +0.1335 °C per decade for India, +0.1804 °C per decade for China, and +0.2385 °C per decade for the United States over 1940–2025.

## Limitations

- The modern observations and paleoclimate reconstruction differ in baseline, averaging conventions, coverage, and methods. Raw anomaly values should not be directly treated as measurements on one shared scale.
- Instrumental observations may have contributed to calibration of the reconstruction, so comparison with the instrumental target is not necessarily independent validation.
- The reconstruction's uncertainty interval reflects ensemble spread; it does not by itself establish accuracy. A narrower interval later in the record does not prove that later estimates are more accurate.
- Filtering changes the series and its available endpoints. The notebook notes missing filtered values near the reconstruction endpoint; endpoint behavior should be interpreted cautiously.
- Trend estimates and statistical inference depend on model choices. HAC standard errors and the tested lag sensitivity address some autocorrelation concerns but do not cover every possible time-series specification. The candidate breakpoint search is exploratory and is not, by itself, a formal test of a physical regime change.
- Period averages and temperature records alone do not establish causes of climate change or ecological effects. Historical comparisons are descriptive.

## Reproducing the analysis

Use the finalized notebook as the primary entry point. Keep the three data files in the same directory as the notebook, start Jupyter from that directory, and execute cells in order. The notebook includes saved outputs; running it will recalculate those outputs.

The analysis uses Python 3 and imports these packages: pandas, NumPy, Matplotlib, SciPy, scikit-learn, and statsmodels. In an environment with Python and Jupyter installed, the required analysis packages can be installed with:

```bash
python -m pip install pandas numpy matplotlib scipy scikit-learn statsmodels
```

Files required by the finalized notebook for a full reproduction:

1. `Climate_Variability_and_Environmental_Resilience_Finalized.ipynb`
2. `annual-temperature-anomalies.csv`
3. `average-annual-surface-temperature.csv`
4. `Full_ensemble_median_and_95pct_range.txt`

The earlier notebook also uses all three data files. Jupyter checkpoint files, if present under `.ipynb_checkpoints/`, are automatic working copies and are not required to reproduce the analysis.

## Publication file review

The finalized notebook and all three data files listed above are needed for the complete analysis. The earlier notebook is useful context but is not required if using the finalized notebook. The checkpoint directory contains automatic copies and is not needed for publication or reproduction; it can be excluded from a future GitHub upload without changing research files.

The largest files are the two notebooks at about 2.9 MB each; each CSV is about 0.5 MB, and the reconstruction text file is about 0.1 MB. These are modest sizes and are used to preserve saved notebook outputs or reproduce the analysis. A scan of the project text and notebook content for common credential patterns and personal email addresses found no matches. This is a pattern-based check, not a guarantee that every form of sensitive information has been detected.

At the time this README was prepared, the project directory was not initialized as a Git repository. No GitHub repository was created, and no files were committed or pushed.

## Notebook preservation

Both notebooks are retained with their saved outputs. This README documents the existing analysis; it does not replace the notebooks or their recorded results.
