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

## SpO2 -Daily percentage above, below, within SpO2 target
Operational definition = What proportion of patients receiving oxygen therapy who have SPO2 targets set are above, below and in range of their target on a weekly basis?

### GROUP PATIENT HOURLY DATA INTO CALENDAR DAY 
1. Group patient (MRN/CSN) hourly data into a calendar day
   
### GENERATE LABEL FOR 1 HOUR EPOCH & DISCARD ‘IN’-ELIGIBLE HOURS 
1. If more than one SpO2 reading in a one hour epoch, take last reading and discard others 
2. Discard the following hour epoch labels:
     - ‘n/a’ (not on oxygen therapy)
     - ‘fall through’
     - ‘not set’
  
### GENERATE DESIGNATION FOR PATIENT CALENDAR DAY - We need to change these to be patient level calendar day first. 

3. Perform a count of the number of eligible hours in that calendar day (eligible hours should only be labelled as: ‘above’, ‘in range’ or ‘below’ target). This is the denominator. 
4. Take most frequent hour count as the calendar day designation IF highest count is ‘above’ or ‘below’ 
5. IF highest count is ‘in range’ AND label is ‘in range’ for ≥50% of eligible readings then calendar day designation = ‘in range’ 
6. IF the most frequent hour count are equal (between all three ‘in range’ and ‘above’ or ‘below’ then calendar day designation = ‘above’ 
7. IF the most frequent hour count is ‘in range’ AND label is ‘in range’ for ≤49.9% of eligible readings then calendar day designation is second most frequent hour count (‘above’ or ‘below’).  
8. IF the most frequent hour count is equal between ‘above’ and ‘below’ then calendar day designation = ‘above’

### GENERATE DATA POINT FOR SPC CHART 
9. ABOVE CHART: generate percentage weekly percentage ‘above’ SpO2 target (i.e.add up all 'above' calendar day designations in that week and divide by 'above'+ 'In range'+ 'below' in that week). Present as percentage.
10. BELOW CHART: generate percentage weekly designation ‘below’ SpO2 target (i.e.add up all 'below' calendar day designations  in that week and divide by 'above'+ 'In range'+ 'below' in that week). Present as percentage
11. IN RANGE CHART: generate percentage weekly designation ‘in range’ SpO2 target(i.e.add up all 'in range' calendar day designations  in that week and divide by 'above'+ 'In range'+ 'below' int that week). Present as percentage


 
