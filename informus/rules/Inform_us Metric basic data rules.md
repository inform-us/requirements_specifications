# Exemplar Metrics Inform_us Data Rules

### These are the data rules and thresholds for the metrics that appear on the inform_us dashboard https://informus.org.uk and are also ICU exemplar ward Power BI dashboards

## Pain 

### Flowsheets used 

Verbal Pain Scale (at rest)	3040104280

Verbal Pain Scale (at movement)	3040104281

CRITICAL CARE PAIN OBSERVATION SCORE	3040104659

The pain tile shows the percentage of documented readings that none or mild in the last 24 hours. 

Denominator = All documented CPOT and VPS scores

Numerator = All documented CPOT and VPS scores that are none or mild

Pain scores documented on time

Pain scores are considered 'on time' if they are documented within 1 hour and 15 minutes (added documentation leeway) after a moderate to very severe score. Otherwise the score is shown as missing. 

Pain scores are considred 'on time if they are documented within 4 hours and 15 minutes (added documentation leeway) after a none or mild score. Otherwise the score is shown as missing

### MEASUREMENT INTERVAL SPC CHARTS 

We also display weekly SPC charts that show what percentage of pain scores are done 'on time' as per guidelines. 
Week defined a Monday 00:00 – Sunday 23:59
Chart 2a GREEN [Measurement Interval Chart] - none to mild pain
Look at GREEN category measurement intervals in that week
Numerator = count of time intervals that are ≤ 4:00 hours for the GREEN category
SPC denominator adjustment required for excessively long measurement intervals (those that are 2x accepted measurement interval from clinical guidance)
Denominator (adjusted) = count all measurement intervals in the GREEN category in that week that are >8:00 hours and ADD +1 to denominator for each four hour period greater than the permitted 4:00 hours
For example: (i) an 8:01hr measurement interval will count as 2 in the adjusted denominator - once for the measurement and once for being an additional 4:00hr over the permitted four hours for this category; (ii) 12:01hr measurement interval will count as 3 in the adjusted denominator; (iii) 16:01hr measurement interval will count as 4 in the adjusted denominator etc...
Generate percentage of measurement intervals for that week that are 4:00 hours or less: numerator / denominator (adjusted)
Plot on weekly chart
Chart 2b AMBER/RED [Measurement Interval chart] - moderate severe pain
Look at AMBER/RED category measurement intervals in that week
Numerator = count of time intervals that are ≤ 1:00 hour for the AMBER/RED category
SPC denominator adjustment required for excessively long measurement intervals (those that are 2x accepted measurement interval from clinical guideance)
Denominator (adjusted) = count all measurement intervals in the AMBER/RED category in that week that are >1:00 hours and ADD +1 to denominator for each one hour period greater than the permitted 1:00 hours
For example: (i) an 2:01hr measurement interval will count as 2 in the adjusted denominator - once for the measurement and once for being an additional 1:00hr over the permitted four hours for this category; (ii) 3:01hr measurement interval will count as 3 in the adjusted denominator; (iii) 4:01hr measurement interval will count as 4 in the adjusted denominator etc...
Generate percentage of measurement intervals for that week that are 1:00 hour or less: numerator / denominator (adjusted)
Plot on weekly chart




