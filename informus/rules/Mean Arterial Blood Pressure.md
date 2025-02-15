# Mean Arterial Blood Pressure (MAP) rules
Rules for Mean Arterial Blood Pressure (MAP) metric

## EPIC Flowsheets

Flowsheet update - all volume flowsheets in ml

Vasopressors:
3040102622 noradrenaline
331213 adrenaline
12946 metaraminol
7080040 vasopressin
7071002 terlipressin

Inotropes:
331213 adrenaline
331208 dobutamine
25239 levosimenden
12536 enoximone
331253 milrinone

Antihypertensives:
12812 hydralazine
331203 GTN
3040101268 labetalol
25251 metoprolol
331243 esmolol
331258 SNP


* ### Group ID:
-  [] 

* ### Individual metric Row ID:
| Flowsheet | Row ID | Manual/Automatic/Calculated Input | Comments | Expected documentation frequency|
  |-|-|-|-|-|
  |MAP|301360||||
  |Arterial line MAP|310250| Automatic| Taken from monitor|Hourly (varies according to patient condition)|
  |MAP target| 36554| Manual| Drop down (free text possible)| Minimum once per day between 0800 and 1200|
  |Noradrenaline|3040102622| Manual| Numerical (free text possible) | Hourly|
  |Adrenaline|331213|Manual| Numerical (free text possible)| Hourly|
  



## Validity (time window) Rules: 

1. MAP only valid if map_dt within last 6 hours of epoch_dt 
2. Inotropes only valid if within last 4 hours 
3. 8:00 - 12:00 MAP Target Validity rule: 
  -  if epoch time before 12noon, 
  -  if map_target_dt after 8am on the day before then mark as valid else as invalid 
  -  if epoch after 12noon, 
  -  if map_target_dt after 8am on the morning of then mark as valid else as invalid 

        	 
## Classification Rules: (corresponds to the per patient chart) 

1. if not 'on_inotrope': 'not applicable'
2. if not 'has_valid_map':'missing' 
3. if 'has_valid_numerical_map_target': below or above or in range 
4. if 'has_valid_entered_map_target':'non-numerical 
5. if none of the above 'not set'

## Summary Rules (corresponds to tile data)

### Percentage of readings on Target Calculation
Denominator = the number of MAP readings that have had 'has_valid_numerical_MAP_target': 'below' or 'above' or 'in range' or if 'has_valid_entered_MAP_target': 'non-numerical' set within the last 24 hours
Numerator = the number of these MAP readings that were within their target within the last 24 hours
Denote as percentage

### Total Hours on Vasoactive Drugs Calculation (corresponds to front tile)

Calculate the total patient hours of 'on_inotrope' in the last 24 hours. Exclude any time += one hour when a patient is off the unit, e.g. patient has left the unit for a scan or procedure and has returned.
 
## Labelling Rules: (corresponds to the floor plans)     

1. if the latest 3 consecutive hours are all classified as 'above' then label patient as 'above'
2. if the latest 2 consecutive hours are both classified as 'below' then label patient as 'below'       
3. if the latest classification is 'not applicable' then label the patient as 'not applicable' 
4. if there are 5 non-consecutive hours in the 24hr timeseries classified as *either* 'below' or 'above', count backward and label the patient the majority label 
5. if the latest hour is classified as 'in range', then label patient as 'in range' 
6. if the latest classification is 'non-numerical' then label the patient as 'non-numerical' 
7. if the latest classification is 'missing' then label the patient as 'missing' 
8. if the latest classification is 'not set' then label the patient as 'not set' 
9. if the classification was 'in range' and is now above(below) for fewer than 3(2) hours then label as 'in range' 
10. if none of the rules matched then label the patient as 'fallthrough'
11. n.b. fallthrough is shown as dark grey bed on floorplan, but there is no accompanying legend item. This is explained to user in ? button. 
---
# SPC CHARTS
## Mean Arterial Blood Pressure (MAP) - Daily percentage MAP 
Operational definition = of the patients who are on vasopressor therapy and have had MAP targets set in ICU naviagtors in EPIC, what proportion are above, below and within their MAP targets on a weekly basis? 
### GROUP PATIENT HOURLY DATA INTO CALENDAR DAY 
1. Group patient (MRN/CSN) hourly data into a calendar day 

### GENERATE LABEL FOR 1 HOUR EPOCH & DISCARD ‘IN’-ELIGIBLE HOURS 
2. If more than one MAP reading in a one hour epoch, take last reading and discard others 
3. Discard the following hour epoch labels: 
   - ‘n/a’ (not on vasopressor therapy)
   - ‘fall through’
   -  ‘not set’ 

### GENERATE DESIGNATION FOR PATIENT CALENDAR DAY 
4. Perform a count of the number of eligible hours in that calendar day (eligible hours should only be labelled as: ‘above’, ‘in range’ or ‘below’ target). This is the denominator. 
5. Take most frequent hour count as the calendar day designation IF highest count is ‘above’ or ‘below’ 
6. IF highest count is ‘in range’ AND label is ‘in range’ for ≥50% of eligible readings then calendar day designation = ‘in range’ 
7. IF the most frequent hour count are equal (between all three ‘in range’ and ‘above’ or ‘below' then calendar day designation = ‘above’ 
8. IF the most frequent hour count is ‘in range’ AND label is ‘in range’ for ≤49.9% of eligible readings then calendar day designation is second most frequent hour count (‘above’ or ‘below’).  
9. IF the most frequent hour count is equal between ‘above’ and ‘below' then calendar day designation = ‘above’ 

### GENERATE DATA POINT FOR SPC CHART 
10. Take all of the patient calendar day designations and aggregate into one week: Week defined as: Monday 00:00 - Sunday 23:59 
11. ABOVE CHART: generate percentage weekly designations that are above MAP target = (i.e. add up all ‘above’ in that week and divide by ‘above’ + in range’ + ‘below’ in that week). Present as percentage  
12. BELOW CHART: generate percentage weekly designations that are below MAP target (i.e. add up all ‘below’ in that week and divide by ‘above’ + in range’ + ‘below’ in that week). Present as percentage  
13. IN RANGE CHART:  generate percentage weekly designations that are in range MAP target (i.e. add up all ‘in range’ in that week and divide by ‘above’ + in range’ + ‘below’ in that week). Present as percentage
14. Plot on weekly chart

    

 

 
