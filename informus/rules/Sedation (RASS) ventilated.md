
# SEDATION SCORE (using the Richmond Agitation Sedation Score -RASS) rules

Rules for Sedation (on mechanical ventilation) metric, measured using the RASS scale (sedation/agitation)

## EPIC
- The degree of sedation and conversely agitation are measured by the Richmond Agitation Sedation Score (RASS)
- For the purposes of the RASS metric tile, we are particularly interested in oversedation on mechanical ventilation (i.e. a score more negative than the target set) which has a detrimental impact on length of stay, morbidity & mortality, hence the eligibility criteria include 'is_ventilated' & 'is_sedated')
- RASS runs on 10 point scale from (agitated) +4/+3/+2/+1/0/-1/-2/-3/-4/-5 (sedated) - *see table below*
- RASS scale value is an integer (note EPIC will allow free text!)
- RASS expected charting frequency differs during the day and night: <br> RASS_frequency_DAY: day defined as 06:00:00 - 21:59:59 - hourly as per guideline <br> RASS_frequency_NIGHT: night defined as 22:00:00 - 05:59:59 - 4 hourly as per guideline
- Individual patient RASS target is set on a daily basis [see targets.md](./targets.md#ELIGIBILITY)
- The function of the SEDATION_metric is two-fold: <br> (1) measurement interval - a RASS charting frequency within guidelines <br> (2) achieving set RASS target

___
**The Richmond Agitation Sedation Score**
|Description|Term|Score|
|---|---|---|
|Overtly combative or violent; immediate danger to staff|Combative|+4|
|Pulls on or removes tube(s) or catheter(s) or has aggressive behavior toward staff|Very agitated|+3|
|Frequent non-purposeful movement or patient–ventilator dyssynchrony|Agitated|+2|
|Anxious or apprehensive but movements not aggressive or vigorous|Restless|+1|
|Spontaneously pays attention to caregiver|Alert and calm|0|
|Not fully alert, but has sustained (more than 10 seconds) awakening, with eye contact, to voice|Drowsy|-1|
|Briefly (less than 10 seconds) awakens with eye contact to voice|Light sedation|-2|
|Any movement (but no eye contact) to voice|Moderate sedation|-3|
|No response to voice, but any movement to physical stimulation|Deep sedation|-4|
|No response to voice or physical stimulation|Unarousable|-5|
___

## EPIC Flowshets 

|Flowsheet| Flowsheet ID| Manual/Automatic/Calculation Input| Comments| Expected Documentation Frequency|
|-|-|-|-|-|
|FiO2% | 301550| Manual| Numerical entry (free text option)|Usually hourly but varies depending on patient's clinical condition|
|O2 delivery device| 3040109305|Manual| Drop down (free text option)|Usually hourly but varies depending on patient's clinical condition|
|Vent mode| 3040102607| Manual | Drop down (free text option)|Hourly?|
|RASS score| 3040104644|Manual | Drop down (free text option)|Hourly between 06:00 and 21:59 <br> Fourly hourly between 22:00 and 05:59|
|RASS target| 36555| Manual|  ICU Navigator |Daily between 0800 and 13:00 <br> On admission|
|CLONIDINE| 12351| Manual|  Numerical entry (free text option)|Hourly|
|FENTANYL| 331223| Manual|  Numerical entry (free text option)|Hourly|
|PROPOFOL| 331218| Manual|  Numerical entry (free text option)|Hourly|
|MIDAZOLAM| 3040101274| Manual|  Numerical entry (free text option)|Hourly|
|MORPHINE| 331228| Manual|  Numerical entry (free text option)|Hourly|
|DEXMEDETOMIDINE| 3040101250| Manual|  Numerical entry (free text option)|Hourly|

### Ventilation flowsheet


FIO2_% 301550?
02 Flow rate r ip flowrate 500690?

   "o2delivery": "3040109305",
    "vent_mode": "3040102607",
    "rass_score": "3040104644",
    "rass_target": "36555",
    "CLONIDINE": "12351",
    "FENTANYL": "331223",
    "PROPOFOL": "331218",
    "MIDAZOLAM": "3040101274",
    "MORPHINE": "331228",
    "DEXMEDETOMIDINE": "3040101250"
    
### Group ID Richmond Agitation Sedation Scale (RASS)
- G UCLH ICU NEW NEUROLOGY [39859]

### Row ID RASS
- R RICHMOND AGITATION SEDATION SCALE (RASS) [3040104644]

[SEDATION_user interface sequence .pdf](https://github.com/inform-us/requirements_specifications/files/15480198/SEDATION_user.interface.sequence.pdf)

## ELIGIBILITY
1. Patient (i) on mandatory mechanical ventilation AND (ii) receiving sedative drugs within the last 6 hours
2.  If O2 delivery is endotrachael tube or tracheostomy, patient is on mandatory mechanical ventilation
3.   If ventmode is CPAP/PS...., patient is on mandatory mechanical ventilation
4.    Note in code we seem to be missing the step of classifying what is mandatory ventilation and what is not. We think ventmode set flowsheet.
5.if sedative volume flowsheet is any number (any charted volume), then the patient is sedated. If sedation volume flowsheet is NaN, then patient is not sedated. *note this should be backfilled from 4 hours and looks like current code it isn't*

## Validity (time window) Rules: 
1. O2 delivery device only valid if o2delivery_dt documented within last 6 hours of epoch
2. This is double checked with ventmode flowsheet
3. 
4.*Need to write validity rules here as original code was written with 8 hour leeway. note all early metrics may have extended leeway.* 

### RASS
- clinical guideline recommended charting frequency for RASS differs depending on time of day
- in line with other documentation we add 15 minutes leeway to the validity of the documented score to allow for clinical leeway

### RASS generate 
1) RASS scores documented between 06:00 - 21.59 is valid for 75 minutes
2) RASS scores documented between 22:00 - 05:59 is valid 255 minutes (4 hours & 15 minutes)
   *note current rules have same one hour rule for all day and night*
   
## Summary Rules (corresponds to tile data)

### Percentage of RASS readings on Target Calculation

- Denominator = the number of RASS readings that have had 'has_valid_numerical_rass_target': 'below target', 'above target', 'on target' or 'has_valid_entered_RASS_target': 'non-numerical' set within the last 24 hours
- Numerator = the number of these RASS readings that were 'on target' within the last 24 hours

Denote as percentage

### Total Hours on Sedation (corresponds to front tile)


Calculate the total patient hours of (i) on mandatory mechanical ventilation AND (ii) receiving sedative drugs in the last 24 hours.

Exclude any time += one hour when a patient is off the unit, e.g. patient has left the unit for a scan or procedure and has returned. 

### Measurement Interval - average time between RASS assessments - front tile metric calculation
- this calculation will look at all RASS scores (including those that are not on sedation or mechanically ventilated)
- average time between scores should be calculated from ACTUAL documented RASS scores in EPIC (ie. those with a _dt stamp) and not any forward filled scores
- there needs to be a minimum of two scores to calculate a measurement interval (if a patient has only just been admitted with one RASS score documented, or if a patient only has one RASS score during their entire ICU admission, calculation will not be possible and data will not be included on front tile metric
-  Any period of time where a patient is documented as off unit, e.g. for a scan or procedure, should not factor into the calculation. i.e. if RASS assessment 1 of 2 in an interval has a dt_stamp directly before a time period when the patient is off the unit, this measurement and the interval between dt_stamp 1 and 2, which will occur after the patient has returned back to the unit should be excluded from the average. Time 2 of the interval when the patient returns should therefore become time 1 of the subsequent time interval. This is to avoid excessively long time intervals factoring into the average when there would not have been possible to document a RASS score in the ICU notes. 
- the data on the front tile looks back from the current time to 24 hours in the past
- there will be two measurement interval calculations displayed on the front tile: DAY (06:00-21:59) and NIGHT (22:00-05:59)
- in line with other metrics we should provide some leeway (15 minutes) in charting documentation, therefore (adjusted time frame): DAY (06:00-22:14) and NIGHT (22:00-06:14)
- the leeway is to mitigate skewed mean interval, particularly in the DAY calculation (e.g. 06:01 RASS, time interval calcaulted with a NIGHT RASS at 02:00, would give a 04:01 measurement interval which would skew daytime data, the 15 minute leeway may need to be reviewed if insufficient
- the _dt of each measurement determines whether it is categorised as 'DAY' or 'NIGHT', but in order to complete the measurement interval calculation, a preceeding measurement can be in the opposing category
- worked example: <br> (a) a measurement taken at 06:10 would have to be linked with an earlier measurement during the night shift to calculate an interval and would be classified as - NIGHT (before 06:14) <br> (b) a mesurement taken at 06:30 would have to be linked with an earlier measurement during the day or night shift to calculate an interval and would be classified as - DAY (after 06:14) <br> (c) a mesurement taken at 22:10 would have to be linked with an earlier measurement during the day shift to calculate an interval and would be classified as - DAY (before 22:14) <br> (d) a mesurement taken at 23:00 would have to be linked with an earlier measurement during the night or day shift to calculate an interval and would be classified as - NIGHT (after 22:14) <br>
- once classified into DAY or NIGHT deteremine numerator and denominator for each and calculate mean
- DAY Numerator = sum of the minutes and hours between all intervals recorded between (06:15-22:14) that fall into the current 24 hour rolling window
- DAY Denominator = number of all time interval measurements that fall into the current 24 hour rolling window
- NIGHT Numerator = sum of the minutes and hours between all intervals recorded between (22:15-06:14) that fall into the current 24 hour rolling window
- NIGHT Denominator = number of all time interval measurements that fall into the current 24 hour rolling window
- calculate respective DAY and NIGHT mean measurement interval and display as hh:mm on front tile

## Classification Rules: 
RASS Target set on any day is valid until 12:00hrs the day after the RASS target is set unless another target is set between 08:00 and 12:00hr on the second day. 

1. if 'is_ventilated': 'not applicable' 
2. Add is_sedated check when drugs available 
3. if 'has_valid_rass': missing' 
4. if 'has_valid_numerical_rass_target': 'below target', 'above target', 'on target' 
5. if 'has_valid_entered_rass_target']:'non-numerical' 
6. if non of the above rules: 'not set'

Note if two measurements, take most recent. 



## Labelling Rule: (corresponds to the floor plans)     

1. if latest RASS reading equals target, patient is 'on target' 
2. if latest RASS reading is 'above target' or 'below target', patient is 'off target' 
4. if latest RASS reading 'missing': patient's RASS reading is 'missing' 
5. if RASS target set is false, patient's target is 'not set' 
6. if latest RASS reading is 'not applicable': 'not applicable' 
7. if latest RASS reading 'non-numerical': patient is classified as 'non-numerical' (n.b. assumes free text has been entered into EPIC) 
8. if none of the above: 'fallthrough'
9. n.b. fallthrough is shown as dark grey bed on floorplan, but there is no accompanying legend item. This is explained to user in ? button.

    
---
# SPC CHARTS 
## RASS- Weekly percentage RASS target compliance
Operational definition = of the patients who are ventilated and on sedative drug therapy and have had RASS targets set in ICU navigators in EPIC, what proportion are achieving (‘on’) or not achieving (‘off’) the set RASS target on a weekly basis? 

### GROUP PATIENT HOURLY DATA INTO CALENDAR DAY
1. Group patient (MRN/CSN) hourly data into a calendar day

### GENERATE LABEL FOR 1 HOUR EPOCH & DISCARD ‘IN’-ELIGIBLE EPOCHS 
2. If more than one RASS reading in a one hour epoch, take last reading and discard others 

3. Discard the following hour epoch labels:
    - ‘n/a’ (not ventilated / sedated)
    - ‘fall through’
    - ‘not set’
    - ‘missing’
  
  ### GENERATE DESIGNATION FOR PATIENT CALENDAR DAY 
4. Perform a count of the number of eligible hours in that calendar day (labels: ‘on target’ or ‘off target’). This is the denominator
5. Take most frequent epoch count as the calendar day designation. IF highest count on that calendar day is ‘on target’ then designate as ‘on target’
6. IF highest count on that calendar day is ‘off target’ then designate as ‘off target’
7. IF the most frequent hour counts are equal (between ‘on target’ and ‘off target’ then calendar day designation = ‘on target’

### GENERATE DATA POINT FOR SPC CHART 
7. Take all of the patient calendar day designations and aggregate into one week: Week defined as: Monday 00:00 - Sunday 23:59 
9. Generate weekly percentage designations that are on target (i.e. add up all ‘on target’ in that week and divide by ‘on target’ + ‘off target’ in that week). Present as percentage
10. Plot on weekly chart


## Chart 2 RASS ASSESSMENT TIME INTERVAL SPC CHARTS 

These are weekly percentage (p-charts) SPC.

Operational definition = what percentage of RASS scores are done one time within the 1 hour guidelines (day) and 4 hour guidelines (night)? 

DAY for RASS assessment is defined as between the hours of 06:00am and 21:59pm. Note this is not the same as a 'day shift' used in other metrics (08:00-19:59).  

NIGHT for RASS assessment is defined as between the hours of 22:00pm and 05:59am. Note this is not the same as a 'night shift' used in other metrics (20:00-07:59).

RASS documentation is expected one hourly during the day (06:00-21:59)and 4 hourly during the night (22:00-05:59). 

We apply a 15 minute documentation window to the start of each shift making a day 06:15 start time and end time is 22:14 and a night 22:15 start time and end time is 22:14 and a night  




## Chart 2a - DAY RASS Assessment Time Interval Chart


Day start time is therefore 06:15 and end time is 22:14 to allow for 15 minutes documentation window. 

Modified shift week is therefore Monday 06:15 to Sunday 22:14. 

1.  Look at RASS assessment measurement intervals (for which the first of the pair of measurements in an interval is between the hours of 06:15 and 22:14) each day. Reference measurement interval section above.
2.   Numerator = count of time intervals that are ≤ 1:00 hours for the DAY category
- *note SPC denominator adjustment required for excessively long measurement intervals (those that are 2x accepted measurement interval from clinical guideline)*
  3. Denominator (adjusted) = count all assessment measurement intervals  between the hours of 06:15 and 22:14 in that week that are > 2:00 hours and ADD +1 to denominator for each one hour period greater than the permitted 1:00 hour.

For example: (i) an 2.01hr measurement interval will count as 2 in the adjusted denominator - once for the measurement and once for being an additional 1:00hr over the permitted one hour for this category; (ii) 3.01 hr measurement interval will count as 3 in the adjusted denominator: (iii) 4.01hr measurement interval will count as 4 in the adjusted denominator etc.....
4. Generate percentage of measurement intervals for that week that are 1 hour or less: numerator / denominator (adjusted)
5. Plot on weekly chart

## Chart 2b- NIGHT RASS Assessment Time Interval Chart


Night start time is therefore 22:15 and end time is 06:14 to allow for 15 minutes documentation window. 


1. Look at RASS assessment measurement intervals (for which the first of the pair of measurements in an interval is between the hours of 22:15 and 06:14) each day
2. Numerator = count of time intervals (that are ≤ 4:00 hours for the NIGHT category
- *SPC denominator adjustment required for excessively long measurement intervals (those that are 2x accepted measurement interval from clinical guidance)*
3. Denominator (adjusted) = count all NIGHT assessment measurement intervals in that week that are >8:00 hours and ADD +1 to denominator for each four hour period greater than the permitted 4:00 hours

For example: (i) an 8:01hr measurement interval will count as 2 in the adjusted denominator - once for the measurement and once for being an additional 4:00hr over the permitted four hours for this category; (ii) 12:01hr measurement interval will count as 3 in the adjusted denominator; (iii) 16:01hr measurement interval will count as 4 in the adjusted denominator etc...
4. Generate percentage of measurement intervals for that week that are 4:00 hours or less: numerator / denominator (adjusted)
5. Plot on weekly chart

 

 
   
               
    
