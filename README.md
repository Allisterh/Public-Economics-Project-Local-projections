# Non linear fiscal multipliers with Smooth Transition LP-IV

Course project for Public Economics, University of Bonn (Erasmus, MSc Economics).

The project asks whether the output effect of government spending depends on how progressive the tax system is at the time of the shock. It extends the empirical part of Ferriere and Navarro (2024), "The Heterogeneous Effects of Government Spending: It's All About Taxes", by estimating state dependent cumulative multipliers with a Smooth Transition Local Projection instrumental variable design.

## Data

`Dataset/DATA_MACRO_FN.csv` holds quarterly US series from 1913Q2, taken from the replication material of Ferriere and Navarro: GDP, government spending, the Ramey military news series, and the marginal and average tax rates. The estimation sample ends in 2006Q4.

## Method

The state variable is a measure of tax progressivity, `(MTR - ATR) / (1 - ATR)`, standardised to a z score and passed through a logistic transition with smoothness parameter 3, so that each horizon is estimated as a weighted average of a low progressivity and a high progressivity regime.

Spending is instrumented in three ways, and the three specifications are the point of the exercise:

1. the Ramey military news series,
2. a Blanchard and Perotti shock, recovered as the spending residual of a trivariate VAR in spending growth, output growth and tax revenue growth with four lags, then orthogonalised with respect to the news series,
3. an optimal instrument, the fitted value of a regression of spending growth on both instruments and the controls, which makes the system over identified.

Every specification uses twenty horizons, cumulative multipliers, eight lags of output growth, spending growth and the marginal tax rate as controls, a quartic time trend, and 95 per cent bands. Elasticities are converted into currency multipliers with the sample mean of the output to spending ratio.

## How to run

Open `Public-Economics-Project.Rproj` in RStudio and run `Main_Script.R` from the top. The script needs `dplyr`, `vars`, `lpirfs` and `ggplot2`, and reads the data through a relative path, so the working directory has to be the project folder. It prints the summary of each specification and writes the regime impulse responses and the figures used in the paper.

## What I find

With the news instrument the sign of the heterogeneity matches Ferriere and Navarro, although the magnitudes differ. With the Blanchard and Perotti shock the pattern reverses. With the over identified instrument the two regimes are no longer distinguishable and the multiplier is not significant at the 95 per cent level. The conclusion I draw is that the result is driven by the choice of instrument rather than by the state of the tax system.

## Files

- `Main_Script.R`, the whole estimation from the raw data to the figures.
- `Dataset/`, the input data.
- `Del_Col_PublicEconomics_Project.pdf`, the written project, with the LaTeX source in the folder of the same name.
- `R_Images_LDC/` and `FN_Images/`, my figures and the original ones used for comparison.
