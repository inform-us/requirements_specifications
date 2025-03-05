

# Epidural and Motor Block Assessment 

## Rules for Epidural and the level of motor block that the epidural is providing to the patient

## EPIC

Some patients will be given an epidural for pain management. While epidurals are effective, they also can have complications and carry risk as they can cause temporary paralysis (motor block) which if gone unnoticed for too long can have catastrophic implications including permanent paralysis.It is therefore important for clinical staff to have an overview of who on the units is using an epidural for pain relief and what their level of motor block (temporary paralysis) in order to ensure patient safety. 

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
All patients who have received local anaesthesia via an epidural catheter in the last 12 hours. If a patient has a number equal to or greater than zero entered in flowsheet  Epidural drugs | Volume (mL) | 7001026  within the last 12 hours (use 12 hours for now, but this may be amended), they are eligible. 

*Note these patients will more frequently be found on the post-surgical units, T06 and PACU*

## VALIDITY

A patient is classified as 'on an epidural' for 12 hours following data entry in the flowsheet. 

If a patient is 'on epidural' they are required to have 30415249 Motor block assessment left leg and 30415250 Motor block assessment right leg assessed and documented 2 hourly during the day shift (08:00-19:59), and 4 hourly during the night shift (20:00-07:59). Once there is no data in epidural volume infused flowsheet 7001026, the epidural drugs have been stopped, this pattern of documentation (2 and 4 hours) should be continued for up to 12 hours or until both scores are zero, whichever comes first.


## SUMMARY (tile)


## CLASSIFICATION

### Number of patients on epidural

The epidural data on the front tile is a real-time view of (a) the number of patients who are on an epidural (using the above eligibility criteria of volume infused within the last 12 hours) shown as a number (at each refresh looks back and collect all the current epidural flowsheets), (b) the average time between motor block assessments. 

Calculate the number of patients who are currently on the unit and have had a number equal to or greater than zero in epidural volume flowsheet 7001026 documented in the last 12 hours. Discharged patients are not included.

Present this number on the front tile as 'number of patients on epidural'. 

### Average time between motor block assessments (a) Day and (b) night 

Number of patients with an epidural infusion in the last 12 hours 


Aaverage time between motor block assessments (day) (night) in the last 24 hours- front tile metric calculation

This calculation will look at all Motor block assessments for epidural patients. 
The average time between scores should be calculated from ACTUAL documented motor block scores in EPIC (ie. those with a _dt stamp) and not any forward-filled scores

There needs to be a minimum of two scores to calculate a measurement interval (if a patient has only just been admitted with one motor block score documented, or if a patient only has one motor block score during their entire ICU admission, calculation will not be possible and data will not be included on front tile metric.

The data on the front tile looks back from the current time to 24 hours in the past.

There will be two measurement interval calculations displayed on the front tile: DAY (08:00-19:59) and NIGHT (20:00-07:59)
in line with other metrics we should provide some leeway (15 minutes) in charting documentation, therefore (adjusted time frame): DAY (08:15-20:14) and NIGHT (20:15-08:14). The leeway is to mitigate skewed mean interval, particularly in the DAY calculation (e.g. 08:01 motor block assessment, time interval calculated with a NIGHT MOTOR BLOCK at 02:00, would give a 04:01 measurement interval which would skew daytime data, the 15 minute leeway may need to be reviewed if insufficient.

the _dt of each measurement determines whether it is categorised as 'DAY' or 'NIGHT', but in order to complete the measurement interval calculation, a preceding measurement can be in the opposing category worked example:

(a) a motor block assessment documented at 08:10 would have to be linked with an earlier measurement during the night shift to calculate an interval and would be classified as - NIGHT (before 08:14)

(b) an assessment documented at 8:30 would have to be linked with an earlier measurement during the day or night shift to calculate an interval and would be classified as - DAY (after 08:14)

(c) an assessment documented at 20:10 would have to be linked with an earlier measurement during the day shift to calculate an interval and would be classified as - DAY (before 20:14)

(d)an assessment documented 20:00 would have to be linked with an earlier measurement during the night or day shift to calculate an interval and would be classified as - NIGHT (after 20:14)

 - Once classified into DAY or NIGHT, determine numerator and denominator for each and calculate mean
 - DAY Numerator = sum of the minutes and hours between all intervals recorded between (08:15-20:14) that fall into the current 24 hour rolling window
 - DAY Denominator = number of all time interval measurements that fall into the current 24 hour rolling window
 - NIGHT Numerator = sum of the minutes and hours between all intervals recorded between (20:15-08:14) that fall into the current 24 hour rolling window
 - NIGHT Denominator = number of all time interval measurements that fall into the current 24 hour rolling window
calculate respective DAY and NIGHT mean motor block assessment measurement interval and display as hh:mm on front tile

## [B] Floorplan labelling 


## MOTOR BLOCK ASSESSMENT - EPIDURAL PATIENTS FLOOR PLAN

All patients who have been on an epidural infusion running in the last 12 hours need to have their level of motor block (level of paralysis) assessed 2 hourly in the day and 4 hourly in the day. 


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
*In addition to the last documented Motor Block Assessment, we need to display whether a motor block assessment is overdue (missingness). If a Motor Block Assessment is overdue, we need know what the last reading was as well. 

1. If there has never been an 'Assessment of Motor Block Lt leg' or 'Assessment of Motor Block Rt leg assessment' since the patients has been classified as 'on epidural', then label patient as 'missing assessment'. Red Hashed and no fill bed.  
2. If the current time is 08:00-19:59, if either 'Assessment of Motor Block Lt leg' or 'Assessment of Motor Block Rt leg assessment' have not been completed in the last two hours, then label patient as 'missing' and forward fill the latest motor block assessment reading (red amber green). Bed to be red hashed outline (with fill of colour from forward filled entry). 
3. If the current time is 20:00-07:59, if either 'Assessment of Motor Block Lt leg' or 'Assessment of Motor Block Rt leg assessment' have not been completed in the last four hours, then label patient as 'missing' and forward fill the latest motor block assessment reading (red amber green). 
Bed to be red hashed outline  (with fill of colour from forward filled entry).
_______________________________________________

## [F] Classification Rules: Individual patient chart

- X-axis time in hours, range 0-72 hours, default to 24 hours
- Y-axis left is motor block assessment score (0 to 3) with 0 denoting no paralysis and 3 denoting full paralysis of either leg.
- Use rules on lines 110-115 to determine classification for individual charts

   

### DESIGN KEY FOR INDIVIDUAL CHARTS

a. Label data points as circles

b. Missing – no data points with grey bar

c. Colour code – RAG rated motor block assessment score 

d. 0-1 = GREEN filled

e. 2= AMBER filled

f. 3 =RED filled

g. X on x axis to denote patient not on epidural in the last 12 hours. 


## DRAFT below- 

## [D] SPC CHARTS

Operational definition - For patients on epidurals, what percentage of motor block assessments are done on time as per guidelines. Chart a- day, Char b- night. 

Measurement Interval (for motor block assessment scoring only)
Average time between motorblock assessments - note suggest not on front tile- TBC. 

ABC SPC CHARTS (refer to XYZ metric in classification

Calendar day defined as 00:00 - 23:59
Week defined as Monday 00:00 – Sunday 23:59


These are weekly percentage (p-charts) SPC
Week defined a Monday 00:00 – Sunday 23:59
