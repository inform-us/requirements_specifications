# Rules for qualifying patient labels for Statistical Process Control (SPC) Charts

(weekly aggregate time series data)

See [Mohammed, Worthington & Woodall; Plotting basic control charts: tutorial notes for healthcare practitioners](https://qualitysafety.bmj.com/content/17/2/137) for mathematical background.

## About SPC Percentage Charts (p-charts)
A p-chart is a time series chart showing a percentage with three reference lines - a mean, and an upper (UCL) and lower control limit (LCL) which indicate that 99% of the data points fall within these two limits. SPC charts are used in Quality Improvement to view variation in a process over time and to assess whether changes that are made to processes during improvement initiatives are resulting in actual statistically meaningful improvements (rather than common cause variation).

# Constructing the charts

* Build y-axis depicting the variable in question (the performance indicator you are interested in)
* Build x-axis depicting time in days/weeks
* Default x-axis to show last 52 data points, slider to allow up to 112 data points
* Database to hold 164 data points to allow annual export (manual) of data from DBForge; older data than this can be automatically erased
* Data points [Label: standard data point = blue dots; trend = blue squares; shift = organge diamonds; outlier = red triangle]
* Build central line based on the mean of all data points [Label: red line]
* Build upper and lower control limits [Label: green hashed line] to the data 3 sigma (σ) above and below the mean

## Formulae for calculating process mean and control limits

n = sample size (e.g. all patients)

x = number of events we are interested in (e.g. patients on target)

Process mean:

$\bar{p} = \frac{\sum x_i}{\sum n_i}, i=1...n$

Sigma is a measure of the variation of a binomial distribution, calculated as the square root of the process mean x (1-process mean) / n

$\sigma = \sqrt{\bar{p}(1 - \bar{p}) / n_i}$

Upper and lower control limits are 3 sigma above and below the process mean, but can't be below 0% or above 100%

Upper control limit = $\bar{p} + 3 \sigma$ (capped at 100%)

Lower control limit = $\bar{p} - 3 \sigma$ (capped at 0%)



## Rules for detecting special cause variation, i.e. statistically meaningful variation in the process

## Rule 1 - SHIFT 

When an SPC chart shows at least 7 data points above or below the mean, denote as a shift using 7 orange diamonds  

## Rule 2 - TREND  

When an SPC chart shows at least 7 ascending or descending data points, denote as a trend using 7 blue squares  

## Rule 3- OUTLIER 

When an SPC chart shows any data point outside of the control limits, denote as an outlier using a red triangle  

Note: *Control limits are stepped as they reflect the change in sample size of each data point* 

- If data points indicate a TREND as well as a  SHIFT, denote as SHIFT only. 
- If data points indicate a TREND which includes an OUTLIER, denote all nonoutlier data points as a TREND (blue squares) and denote any outlier data points OUTLIERS (red triangle) within the TREND. 
- If data points indicate a SHIFT which includes an OUTLIER, denote all nonoutlier data points as a SHIFT (orange diamonds) and denote outlier data points as OUTLIERS (red triangle) within the SHIFT. 

## Mean recalculation
If 11 + 1 consecutive data points above or below the mean (=shift plus 5 more points), then recalculate the mean from the 12th data point using those 12 data points (i.e. this point and the preceding 11), but visually depict a change in mean going forward from the 12th data point. Note that outliers that are above or below the mean should be included in this calculation. 
If there has been no mean recalculation at the end of a three month period: (end defined as March 31st, June 30th, September 30th & December 31st), then automatically recalculate mean using the previous 13 data points, only visually display change in mean going forward on next data point

