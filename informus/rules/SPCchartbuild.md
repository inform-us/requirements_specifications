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

## Mean and process limit recalculation

If 11 + 1 consecutive data points above or below the mean including outliers (=shift plus 5 more points), then recalculate the mean and process limits using those preceding 12 data points (i.e. the 12th point and the preceding 11). Visually depict the recalculated mean and process limits going forward from the 12th data point. 

*Note that outliers that are above or below the mean should be included in this calculation even if they aren't depicted as part of a shift as they are outliers as they lie above or below the process limit.* 

If there has been no data-driven mean and process limit recalculation at the end of 26-week (6 month) period: then automatically recalculate the mean and process limits from the 26th data point and the preceding 23 data points. Visually depict the recalculated mean and process limits going forward from the 26th data point. 

## Establishing a baseline mean for new SPC charts

When a new SPC chart is made, the mean and process limits are considered 'floating' because there really isn't enough baseline data to calculate an average of the data or its limits with any certainty. To account for this and also find balance between waiting for too long to display a mean... we apply these rules for new SPC charts. 

Calculate a baseline mean and process limits using the following: 

1. In week one- data point one
2. In Week two- the mean of data point one and two
3. In week three- the mean of data point one, two and three
4. In week four- the mean of data point one, two, three and four

The week four mean and process limits become our baseline mean and limits. After week four the mean and process limits should be held as constant until one of the mean recalculation rules is triggered, e.g. it has been 26 weeks or there have been 12 points above or below the mean from week four (our baseline mean).
