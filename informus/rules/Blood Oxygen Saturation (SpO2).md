# Blood Oxygen Saturation (SpO2) rules 
Rules for Blood Oxygen Saturation metric


## EPIC Flowsheets

* ### Group ID:
-  [] 

* ### Individual metric Row ID:
| Flowsheet | Row ID | Manual/Automatic/Calculated Input | Comments | Expected documentation frequency|
  |-|-|-|-|-|
  |Oxygen saturation|10|Automatic| Taken from monitor| Hourly (varies according to patient's clinical condition)|
  |O2 flow rate| 250026| Manual | Numerical entry (free text possible)| Hourly only if FiO2 not documented|
  |FiO2%|301550|Manual| Numerical entry (free text possible)| Usually Hourly (Vaires according to clincial condition|
  |R UCLH ICU TARGETS SPO2|36551| Manual| Drop down (free text possible)| minimum once per day between 0800 and 1200|

## Validity (time window) Rules: 

1. O2Sat only valid if o2sat_dt within last 4 hours of epoch 

2. FiO2% only valid if within last 4 hours AND > 21	 

3. Flowrate only valid if within last 4 hours	 

4. 8:00 - 12:00 spo2 Target Validity rule: 
- if epoch time before 12noon: 
- if spo2target_dt after day before 8am then mark as valid else as invalid 
- if epoch after 12noon: 
- if spo2target_dt after 8am the morning of then mark as valid else as invalid 



## Classification Rules: (corresponds to the per patient chart) 

1. if 'on_room_air': 'not applicable'
2. if 'has_valid_o2sat': 'missing'
3. if  'has_valid_numerical_spo2_target': 'below' or 'above' or 'in range' 
4. if 'has_valid_entered_spo2_target': 'non-numerical'
5. if none of the above:  'not set'

   assign an epoch to each existing dt, a measurement within an hour and assigning it to the previous hour. 


## Summary Rules (corresponds to tile data)

### Percentage of readings on Target Calculation

- Denominator = the number of SP02 readings that have had 'has_valid_numerical_spo2_target': 'below' or 'above' or 'in range' 
or if 'has_valid_entered_spo2_target': 'non-numerical' set within the last 24 hours
- Numerator = the number of these SPO2 readings that were within their target within the last 24 hours
- Denote as percentage

### Total Hours on Oxygen Therapy Calculation
  
- Calculate the total patient hours of'on_room_air': 'not applicable' in the last 24 hours. Exclude any time += one hour when a patient is off the unit, e.g. patient has left the unit for a scan or procedure and has returned. 

## Labelling Rule: (corresponds to the floor plans)     

 1. if the latest 3 consecutive hours are all classified as 'above' then label patient as 'above' 
 2. if the latest 2 consecutive hours are both classified as 'below' then label patient as 'below'            
 3. if the latest classification is 'not applicable' then label the patient as 'not applicable' 
 4. if there are 5 non-consecutive hours in the 24hr time series classified as *either* 'below' or 'above', count backward and label the patient the majority label 
 5. if the latest hour is classified as 'in range', then label patient as 'in range' 
 6. if the latest classification is 'non-numerical' then label the patient as 'non-numerical' 
 7. if the latest classification is 'missing' then label the patient as 'missing' 
 8. if the latest classification is 'not set' then label the patient as 'not set' 
 9. if the classification was 'in range' and is now above(below) for fewer than 3(2) hours then label as 'in range'
 10. if the patient has been off the unit for += 1 hour, e.g. for imaging or a procedure, exclude these hours from this calculation
 11. if none of the rules matched then label the patient as 'fallthrough'

---
# SPC CHARTS

## NOTE
Calendar week defined as: Monday 00:00 - Sunday 23:59:59
Data required: (i) number of patients (ie. CSN); (ii) 1-hour epoch labels (above/in range/below)

## SpO2 - Weekly percentage above, below, within SpO2 target
Operational definition = What proportion of patients receiving oxygen therapy (who have SPO2 targets set) are above, below and in range of their target on a weekly basis?
 
### 1 HOUR EPOCHS & DISCARD ‘IN’-ELIGIBLE HOURS 
1. 1-hour epochs from labelling rules above
2. Discard the following epoch labels:
     - ‘n/a’ (not on oxygen therapy and therefore not eligible to be in this metric calcaulation)
     - ‘fall through’
     - ‘not set’ (no target set)

### Percentage calculation
1. Fetch data from the previous calendar week
2. Number of patients: find the individial patient episodes (CSN; ie. the number of individial patients who were on each respective unit during that week)
3. Find the corresponding 1-hour epch labels for each individial patient (only labels are: above/in range/below) within that calendar week

4. ABOVE
- **Numerator** = count of the number of 1-hour epochs labelled as 'above' (for each patient - CSN)
- **Denominator** = count of the number of 1-hour epochs labelled as 'above', ‘in range’ and ‘below’ (for each patient - CSN)
- Calculate the individual patient (CSN) percentage for the calendar week = numerator / denominator
- Aggregate all the weekly patient percentages and divide by the number of patients (point 2 above) to generate an **aggregated weekly percentage mean** of 'the proportion of patients receiving oxygen therapy who are 'above' target - **this is the SPC data point**
- Plot an SPC chart for: y-axis = weekly percentage; x-axis = time

5. IN RANGE
- **Numerator** = count of the number of 1-hour epochs labelled as 'in range' (for each patient - CSN)
- **Denominator** = count of the number of 1-hour epochs labelled as 'above', ‘in range’ and ‘below’ (for each patient - CSN)
- Calculate the individual patient (CSN) percentage for the calendar week = numerator / denominator
- Aggregate all the weekly patient percentages and divide by the number of patients (point 2 above) to generate an **aggregated weekly percentage mean** of 'the proportion of patients receiving oxygen therapy who are 'in range' of target - **this is the SPC data point**
- Plot an SPC chart for: y-axis = weekly percentage; x-axis = time

6. BELOW
- **Numerator** = count of the number of 1-hour epochs labelled as 'below' (for each patient - CSN)
- **Denominator** = count of the number of 1-hour epochs labelled as 'above', ‘in range’ and ‘below’ (for each patient - CSN)
- Calculate the individual patient (CSN) percentage for the calendar week = numerator / denominator
- Aggregate all the weekly patient percentages and divide by the number of patients (point 2 above) to generate an **aggregated weekly percentage mean** of 'the proportion of patients receiving oxygen therapy who are 'below' target - **this is the SPC data point**
- Plot an SPC chart for: y-axis = weekly percentage; x-axis = time

7. Repeat for each respective unit T03/GWB/T06/WMS

8. SPC title would need to be adjusted to 'Weekly percentage DURATION of patients within / above / below SpO2 Saturations Target (patients on oxygen therapy)

### n-number for process limits

n-number for process limits = number of individial patients (CSN) who were on each respective unit during that week (point 2 above)

**Tooltip display = process limit n-number and labelled as 'eligible patients' 

> [!NOTE]
> Check tooltip is correct.
