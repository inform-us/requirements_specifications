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

1. MAP only valid if map_dt within last 4:15 hours of epoch_dt 
2. Inotropes only valid if within last 6 hours 
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

## NOTE

Calendar week defined as: Monday 00:00 - Sunday 23:59:59

Eligible patients: only patients who meet eligibility rules above (i.e meet criteria for 'on inotrope').

Data required: (i) number of eligible patients (ie. CSN that meet above criteria); (ii) 1-hour epoch labels ('above' / 'in range' / 'below')

## Mean Arterial Blood Pressure (MAP) - Weekly percentage above, below, within SpO2 target
Operational definition = What proportion of patients receiving VASOACTIVE DRUG therapy (who have MAP targets set) are above, below and in range of their target on a weekly basis?

### 1 HOUR EPOCHS & DISCARD ‘IN’-ELIGIBLE HOURS 
1. 1-hour epochs from labelling rules above
2. Discard the following epoch labels:
     - ‘n/a’ (not 'on inotrope' and therefore not eligible to be in this metric calcaulation)
     - ‘fall through’
     - ‘not set’ (no target set)

### Percentage calculation
1. Fetch data from the previous calendar week
2. Number of patients: find the individual patient episodes (CSN; ie. the number of individual patients who were on each respective unit during that week)
3. Find the corresponding hourly epoch labels for each individual patient (only labels are: above/in range/below) within that calendar week

4. ABOVE
- **Numerator** = count of the number of 1-hour epochs labelled as 'above' (for each patient - CSN)
- **Denominator** = count of the number of 1-hour epochs labelled as 'above', ‘in range’ and ‘below’ (for each patient - CSN)
- Calculate the individual patient (CSN) percentage for the calendar week = numerator / denominator
- Aggregate all the weekly patient percentages and divide by the number of patients who contributed to above calculation to generate an **aggregated weekly percentage mean** of 'the proportion of patients receiving vasoactive therapy who are 'above' target - **this is the SPC data point**
- Plot an SPC chart for: y-axis = weekly percentage; x-axis = time

5. IN RANGE
- **Numerator** = count of the number of 1-hour epochs labelled as 'in range' (for each patient - CSN)
- **Denominator** = count of the number of 1-hour epochs labelled as 'above', ‘in range’ and ‘below’ (for each patient - CSN)
- Calculate the individual patient (CSN) percentage for the calendar week = numerator / denominator
- Aggregate all the weekly patient percentages and divide by the number of patients who contributed to in range calculation to generate an **aggregated weekly percentage mean** of 'the proportion of patients receiving vasoactive therapy who are 'in range' of target - **this is the SPC data point**
- Plot an SPC chart for: y-axis = weekly percentage; x-axis = time

6. BELOW
- **Numerator** = count of the number of 1-hour epochs labelled as 'below' (for each patient - CSN)
- **Denominator** = count of the number of 1-hour epochs labelled as 'above', ‘in range’ and ‘below’ (for each patient - CSN)
- Calculate the individual patient (CSN) percentage for the calendar week = numerator / denominator
- Aggregate all the weekly patient percentages and divide by the number of patients who contributed to below calculation to generate an **aggregated weekly percentage mean** of 'the proportion of patients receiving vasoactive therapy who are 'below' target - **this is the SPC data point**
- Plot an SPC chart for: y-axis = weekly percentage; x-axis = time

7. Repeat for each respective unit T03/GWB/T06/WMS

8. SPC title would need to be adjusted to 'Weekly percentage DURATION of patients within / above / below MAP Target (patients on vasoactive)

### n-number for process limits

ABOVE = number of individial patients (CSN) who who contributed to above calculation on each respective unit during that week

IN RANGE = number of individial patients (CSN) who who contributed to in range calculation on each respective unit during that week

BELOW = number of individial patients (CSN) who who contributed to below calculation on each respective unit during that week

**Tooltip display = process limit n-number and labelled as 'eligible patients' 

> [!NOTE]
> Check tooltip is correct.

 
