

# Epidural and Motor Block Assessment 

## Rules for Epidural and the level of motor block that the epidural is providing to the patient

## EPIC

All patients who have been on an epidural in (the last twelve hours) need to have an assessment of their 
level of motor block to their right and left leg 2 hourly in the day (08:00-19:59) and 4 hourly in the 
night (20:00-07:59). Once patient's epidural has been stopped, motor block assessment must continue until 
12 hours have passed or both motor block scores are zero, whichever comes first. 

Some patients will be given an epidural for pain management. While epidurals are effective, they also can 
have complications and carry risk as they can cause temporary paralysis (motor block) which if gone unnoticed 
for too long can have catastrophic implications including permanent paralysis.It is therefore important for 
clinical staff to have an overview of who on the units is using an epidural for pain relief and what their 
level of motor block (temporary paralysis) in order to ensure patient safety. 

All patients who have been on an epidural in (the last twelve hours) need to have an assessment of their level of motor block to their right and left leg 2 hourly in the day (08:00-19:59) and 4 hourly in the night (20:00-07:59).

The motor block assessment metric will have its own tile, floor plan and individual chart. Additionally, an icon indicating which patients are on an epidural will also be included on the pain floor plan. 

There will be two SPC charts of the Percentage of Motor Block Assessments done on time as per guidelines (A- Day and B- Night). 

## EPIC Flowsheets

Flowsheet	Row ID | Manual/Automatic/Calculated Input | Comments	| Expected documentation frequency

### Motor Block Assessment

| Tile | Metric | Flowsheet ID | `star.has_visit_observation` is `True` | `star.is_real_time` is `True`  | frequency of reporting | Found in `star.visit_observation_type` | Notes | Status |
|-|-|-|-|-|-|-|-|-|
| Epidural | Assessment of Motor Block Lt leg | 30415249 | ✅ | ✅ | 2-hourly between 0800-1959, 4-hourly between 2000-0759 | ✅ |  | complete (flowsheet is in EMAP) |
| Epidural | Assessment of Motor Block Rt leg | 30415250 | ✅ | ✅ | 2-hourly between 0800-1959, 4-hourly between 2000-0759 | ✅ |  | complete (flowsheet is in EMAP) |



### Epidural infusion volume

| Tile | Metric | Flowsheet ID | `star.has_visit_observation` is `True` | `star.is_real_time` is `True`  | frequency of reporting | Found in `star.visit_observation_type` | Notes | Status |
|-|-|-|-|-|-|-|-|-|

| Epidural drugs | Volume (mL) | 7001026 | ✅ | ✅ | hourly | ✅ |  | complete (flowsheet is in EMAP) |

*note that we cannot get the drugs directly so we use volume infused for a proxy for patient 'on epidural'* 


## ELIGIBILITY

All patients who have received local anaesthesia via an epidural catheter in the last 12 hours. 
If a patient has a number equal to or greater than zero entered in flowsheet  
Epidural drugs | Volume (mL) | 7001026  within the last 12 hours (use 12 hours for now, but this may be amended), they are eligible. 

*Note these patients will more frequently be found on the post-surgical units, T06 and PACU*

## VALIDITY

A patient is classified as 'on an epidural' for 12 hours following data entry in the flowsheet 7001026. 

If a patient is 'on epidural' (i.e. any data entered into flowsheet 7001026 in the last 12 hours) 
they are required to have a motor block assessment documented for at least 12 hours following any data 
entered into flowsheet or until both the right and left motor block assessment scores are '0'. 
The required frequency of documentation is 2 hourly during the day shift (08:00-19:59), and 4 hourly 
during the night shift (20:00-07:59). 



## [A] Front Tile Metric (tile)

## CLASSIFICATION


### Number of patients on epidural

The epidural data on the front tile is a real time view of (a) the number of patients who are on an epidural (using above eligibility criteria of volume infused within the last 12 hours) shown as a number (at each refresh looks back and collect all the current epidural flowsheets), (b) the average time between motor block assessments. 


Calculate the number of patients who are currently on the unit and have had a number equal to or greater than zero in epidural volume flowsheet 7001026 documented in the last 12 hours. Discharged patients are not included.

Present this number on the front tile as 'number of patients on epidural'. 


### Measurement Interval - average time between motor block assessments (a) Day and (b) night (front tile metric)

**NOTE**
1. Average time between scores should be calculated from ACTUAL documented MOTOR BLOCK ASSESSMENTS in EPIC (ie. those with a _dt stamp) and not any forward filled scores.
2. There needs to be a minimum of two scores to calculate a measurement interval (if a patient has only just been admitted with one MOTOR BLOCK ASSESSMENT documented, or if a patient only has one MOTOR BLOCK ASSESSMENT during their entire ICU admission, calculation will not be possible and data will not be included on front tile metric.
3. RIGHT & LEFT motor block assessments are in separate flowsheets and may have different _dt for an asessment done simultaneously in a clinical setting.
4. Any period of time where a patient is documented as off unit, e.g. for a scan or procedure, should not factor into the calculation (see RASS measurement interval rules).
5. The data on the front tile looks back from the current time to 24 hours in the past.
6. There will be two measurement interval calculations displayed on the front tile: DAY (08:00-19:59) and NIGHT (20:00-07:59)
7. In line with other metrics we should provide some leeway (15 minutes) in charting documentation, therefore (adjusted time frame): DAY (08:00-20:14) and NIGHT (20:00-08:14). The leeway is to mitigate skewed mean interval, particularly in the DAY calculation
8. Despite the case that after an epidural has been stopped (i.e. there is no data entered into flowsheet 7001026) and both scores have resumed to zero, motor block assessment is no longer required [on the floorplan view]. The measurement interval calculation is independent of this and does not take into consideration documented scores. Nor does it apply time penalties for extended time intervals (adjusted DENOMINATOR) as is the case in the SPC calculation. 

**CALCULATION**
- this calculation will look at the _dt of MOTOR BLOCK ASSESSMENTS, handling RIGHT and LEFT seprarately before providing a combined average

*RIGHT MOTOR BLOCK ASSESSMENT MEASUREMENT INTERVAL**
- DAY Numerator = sum of the minutes and hours between all intervals recorded between (08:15-22:14) that fall into the current 24 hour rolling window
- DAY Denominator = number of all time interval measurements that fall into the current 24 hour rolling window
- NIGHT Numerator = sum of the minutes and hours between all intervals recorded between (20:15-08:14) that fall into the current 24 hour rolling window
- NIGHT Denominator = number of all time interval measurements that fall into the current 24 hour rolling window

*LEFT MOTOR BLOCK ASSESSMENT MEASUREMENT INTERVAL**
- DAY Numerator = sum of the minutes and hours between all intervals recorded between (08:15-22:14) that fall into the current 24 hour rolling window
- DAY Denominator = number of all time interval measurements that fall into the current 24 hour rolling window
- NIGHT Numerator = sum of the minutes and hours between all intervals recorded between (20:15-08:14) that fall into the current 24 hour rolling window
- NIGHT Denominator = number of all time interval measurements that fall into the current 24 hour rolling window

**COMBINED MOTOR BLOCK ASSESSMENT MEASUREMENT INTERVAL**

- average time interval between RIGHT & LEFT per patient and average count of measurements between RIGHT & LEFT per patient, to produce a single measurement interval and data point (count)

- DAY_AVERAGE_NUMERATOR  - average time interval between (eligible) patients
- DAY_AVERAGE_DENOMINATOR  - average total time interval count between (eligible) patients

- NIGHT_AVERAGE_NUMERATOR  - average time interval between (eligible) patients
- NIGHT_AVERAGE_DENOMINATOR  - average total time interval count between (eligible) patients

- Calculation: numerator / denominator for DAY & NIGHT respectively and display as hh:mm on front tile


REWORK THIS SECTIONF FOR FLOWPLAN USE

Despite the case that after an epidural has been stopped (i.e. there is no data entered into flowsheet 7001026) and both scores have resumed to zero, motor block assessment is no longer required [on the floorplan view]. The measurement interval calculation is independent of this and does not take into consideration documented scores. Nor does it apply time penalties for extended time intervals (adjusted DENOMINATOR) as is the case in the SPC calcaultion.



## [B] Floorplan labelling 

## MOTOR BLOCK ASSESSMENT - EPIDURAL PATIENTS FLOOR PLAN

All patients who have been on an epidural in the last 12 hours are required to have a motor block assessment documented for at least 
12 hours following any data entered into flowsheet or until both the right and left motor block assessment scores are '0'.


ELIGIBILITY

All patients with an epidural volume infused in the last 12 hours. 

*Patients with epidurals to be visually highlighted. Others are not included in the calculation*


## Primary Label Assessment of Motor Block 


1. If either the latest 'Assessment of Motor Block Lt leg' or 'Assessment of Motor Block Rt leg assessment' entry is  0 or 1, label patient as 'motor block = 0 or 1'; GREEN
2. If either the latest 'Assessment of Motor Block Lt leg' or 'Assessment of Motor Block Rt leg assessment' entry is 2, label patient as 'motor block = 2'; AMBER
3. If either the latest 'Assessment of Motor Block Lt leg' or 'Assessment of Motor Block Rt leg assessment' entry is 3, label patient as 'motor block= 3'; RED
4. If both 'Assessment of Motor Block Lt leg' or 'Assessment of Motor Block Rt leg assessment 'measurements have the same _dt stamp, then retain the highest score for that time _dt stamp.
5. If there is an equal highest score (with the same _dt stamp) across 'Assessment of Motor Block Lt leg' or 'Assessment of Motor Block Rt leg assessment '1-hour epoch label, display Rt leg score. 
6. If there are two or more scores in a 1-hour epoch then take the most recent score.


## Secondary Label Assessment of Motor Block 

*In addition to the last documented Motor Block Assessment, we need to display whether a motor block assessment is overdue (missingness). If a Motor Block Assessment is overdue, we need need to display both the last motor block assessment reading and that the score is overdue.* 

1. If there has never been an 'Assessment of Motor Block Lt leg' or 'Assessment of Motor Block Rt leg assessment' since the patient has been classified as 'on epidural', then label patient as 'missing assessment'. Red Hashed and no fill bed.  
2. If the current time is 08:00-19:59, and if either the latest documented motor block score (r or l leg) was >0, and 'Assessment of Motor Block Lt leg' or 'Assessment of Motor Block Rt leg assessment' have not been completed in the last two hours, then label patient as 'missing' and forward fill the latest motor block assessment reading (red amber green). Bed to be red hashed outline (with fill of colour from forward filled entry).
4. If the current time is 20:00-07:59, and if either the latest documented motor block score (r or l leg) was >0, and if either 'Assessment of Motor Block Lt leg' or 'Assessment of Motor Block Rt leg assessment' have not been completed in the last four hours, then label patient as 'missing' and forward fill the latest motor block assessment reading (red amber green).
5. During both day and night shifts, if the volume infused flowsheet returns zero and the subsequent 1hour-epoch is has no data, and the RIGHT & LEFT motor block asssment is zero, then do no t mark as 'missing once the validity period has passed (day = 2:00 hours and night = 4:00 hours) - the floor plan labe would remain GREEN until the 12 hour 'on epidural' has expired. 

WORKED EXAMPLE (epidural infusion stopped) - FLOORPLAN
A patient's epidural has been stopped at 9:00am (there is no more data in the volume infused flowsheet) and the following assessments are documented:

If the motor block assessments are:
1) 09:00 Motor block r leg = 2, Motor block l leg = 1
2) 11:00 Motor block r leg = 1, Motor block l leg = 1
3) 13:00 Motor block r leg = 1, Motor block l leg = 0
4) 15:00 Motor block r leg = 0, Motor block l leg = 0
5) 19:10 Motor block r leg = 0, Motor block l leg = 0
6) 21:00 Motor block r leg = 1, Motor block l leg = 1

Then the time interval are:
1) 09:00 will be linked to the earlier time, and would be classified as day
2) 11:00 will be linked to the earlier time, and would be classified as day and the time interval is 02:00 hours
3) 13:00 will be linked to the earlier time, and would be classified as day and the time interval is 02:00 hours
4) 15:00 will be linked to the earlier time, and would be classified as day and the time interval is 02:00 hours
5) 19:10 will be linked to the earlier time but will not be highlighted as 'overdue' as it is the second consecutive 0 score and remain GREEN
6) 21:00 will be linked to the earlier time and would be classified (score now positive) as night and the time interval is 01:50 hours

_______________________________________________

## [F] Classification Rules: Individual patient chart

- X-axis time in hours, range 0-72 hours, default to 24 hours
- Y-axis left is motor block assessment score (0 to 3) with 0 denoting no paralysis and 3 denoting full paralysis of either leg.
- Use labeling rules above to determine classification for individual charts

   

### DESIGN KEY FOR INDIVIDUAL CHARTS

a. Label data points as circles

b. Missing – no data points with grey bar

c. Colour code – RAG rated motor block assessment score 

d. 0-1 = GREEN filled

e. 2= AMBER filled

f. 3 =RED filled

g. X on x axis to denote patient not on epidural in the last 12 hours. 


## [D] SPC CHARTS

Operational definition - The percentage of motor block assessments (2 hourly during the day shift and 4 hourly during the night shift) done on time for epidural patients 

There are two SPC charts (A) Day and (B) Night

These are weekly percentage (p-charts) SPC charts

DAY shift week is Monday 08:15 to Sunday 20:14
NIGHT shift week is Sunday 20:15 to Monday 08:14


## Chart 1a - DAY Motor Block Assessment Interval Chart

Day start time is 08:15 and end time is 20:14 to allow for 15 minutes documentation leeway. 

Day shift week is therefore Monday 08:15 to Sunday 20:14.

1.  Look at day shift motor block assessment measurement intervals (for which the first of the pair in the measurement interval is between the hours of 08:15 and 20:14) each day. Reference measurement interval rules for tile calculation above making sure to not include any intervals after both scores have resumed to zero. 
2.   **Numerator** =count of time intervals that are ≤ 2:00 hours for the DAY category
- *note SPC denominator adjustment required for excessively long measurement intervals (those that are 2x accepted measurement interval from clinical guideline)*
  
  3. **Denominator (unadjusted)** = count of all motor block assessment measurement intervals during the day shift
  4. **Denominator (adjusted)** = count all day shift motor block assessment measurement intervals in that week that are > 4:00 hours and ADD +1 to denominator for each measurement interval missed.

For example: (i) an 4.01hr measurement interval will count as 2 in the adjusted denominator - once for the measurement and once for being an additional having missed the next expected measurement; (ii) 6.01 hr measurement interval will count as 3 in the adjusted denominator: (iii) 8.01hr measurement interval will count as 4 in the adjusted denominator etc.....
5. Generate percentage of DAY SHIFT measurement intervals for that day shift week (line 222) that are 2 hour or less: numerator / denominator (adjusted)
 6. SPC data point = weekly aggregated day shift mean of numerator/denominator (adjusted) as percentage

### n number for process limit

 Aggregate day shift weekly sum of point 3 denominator (unadjusted) = count of all motor block assessment measurement intervals during the day shifts in the week 
 
**Tooltip display** = process limit n-number with the label "number of measurements".

## Chart 1b- NIGHT Motor Block Assessment Interval Chart

Night start time is 20:15 and end time is 08:14 to allow for 15 minutes documentation leeway.  

Modified NIGHT shift week is therefore Sunday 20:15 to Monday 08:14


1. Look at night shift motor block assessment measurement intervals (for which the first of the pair in the measurement interval is between the hours of 20:15 and 08:14 each day). Reference measurement interval rules for tile calculation above making sure to not include any intervals after both scores have resumed to zero. 
2. **Numerator** = count of time intervals that are ≤ 4:00 hours for the NIGHT category
- *SPC denominator adjustment required for excessively long measurement intervals (those that are 2x accepted measurement interval from clinical guidance)*
   3. **Denominator (unadjusted)** = count of all motor block assessment measurement intervals during the night shift
4. **Denominator (adjusted)** = count all night shift assessment measurement intervals  in that week that are >8:00 hours and ADD +1 to denominator for each measurement interval missed.

For example: (i) an 8:01hr measurement interval will count as 2 in the adjusted denominator - once for the measurement and once for having missed the next expected measurement; (ii) 12:01hr measurement interval will count as 3 in the adjusted denominator
5. Generate percentage of NIGHT shift measurement intervals for that week that are 4:00 hours or less: numerator / denominator (adjusted)
6.  SPC data point = weekly aggregated night shift mean of numerator/denominator (adjusted) as percentage

### n number for process limit

 Aggregate night shift weekly sum of point 3 denominator (unadjusted) = count of all motor block assessment measurement intervals during the night shifts in the week 
 
**Tooltip display** = process limit n-number with the label "number of measurements".

