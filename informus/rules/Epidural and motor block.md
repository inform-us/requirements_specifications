
Deicsion to add icon epidural to pain floor plan and keep motor block fraction on an epidurual, then average time between epidural , then open a individual chart that shows motor block. pick point with the higher 
# Epidural and Motor Block Assessment/Bromage Score Rules

## Rules for Epidural and the level of motor block that the epidural is providing to the patient

EPIC
Some patients will be given an epidural for pain management. While epidurals are effective, they also can have complications and carry risk as they can cause
temporary paralysis (motor block) which if gone unnoticed for too long can have catastrophic implications including permanent paralysis.
It is therefore important for clinical staff to have an overview of who on the units is using an epidural for pain relief and what their 
level of motor block (temporary paralysis) in order to ensure patient safety. 

All patients who have been on an epidural in the last twelve hours need to have Assessment of their level of motor block to their right and left leg (also called the Bromage Score) 2 hourly in the day (08:00-19:59) and 4 hourly in the night (20:00-07:59).

The epidural metric will have its own tile, floor plan and individual chart. An icon indicating which patients are on an epidural will also be included on the pain floor plan. 


There will be two SPC charts of the Percentage of Motor Block Assessments done on time as per guidelines (A- Day and B- Night). 

EPIC Flowsheets
Flowsheet	Row ID | Manual/Automatic/Calculated Input | Comments	| Expected documentation frequency

# Motor Block Assessment/Bromage Score

| Tile | Metric | Flowsheet ID | `star.has_visit_observation` is `True` | `star.is_real_time` is `True`  | frequency of reporting | Found in `star.visit_observation_type` | Notes | Status |
|-|-|-|-|-|-|-|-|-|
| Epidrual | Assessment of Motor Block Lt leg | 30415249 | ✅ | ✅ | 2-hourly between 0800-1959, 4-hourly between 2000-0759 | ✅ |  | complete (flowsheet is in EMAP) |
| Epidural | Assessment of Motor Block Rt leg | 30415250 | ✅ | ✅ | 2-hourly between 0800-1959, 4-hourly between 2000-0759 | ✅ |  | complete (flowsheet is in EMAP) |
| Epidural | LDA line status simple | 3040102506 | ✅ | ✅ |  | ✅ |  | complete (flowsheet is in EMAP) |


# Epidural drugs

| Tile | Metric | Flowsheet ID | `star.has_visit_observation` is `True` | `star.is_real_time` is `True`  | frequency of reporting | Found in `star.visit_observation_type` | Notes | Status |
|-|-|-|-|-|-|-|-|-|

| Epidural drugs | Volume (mL) | 7001026 | ✅ | ✅ | hourly | ✅ |  | complete (flowsheet is in EMAP) |

  |-|-|-|-|-|


ELIGIBILITY
All patients on all units. 
Note these patients will more frequently be found on the post-surgical units, T06 and PACU

VALIDITY
If a patient has data entered in flowsheet  Epidural drugs | Volume (mL) | 7001026  in the last 12 hours, they are classified as 'on epidural'. If a patient is 'on epidural' they are required to have a motor block assessment documented: 2 hourly during the day shift (08:00-19:59), and 4 hourly during the night shift (20:00-07:59). 

CLASSIFICATION

[A] The epidural data on the front tile is a real time view of the number of patients who are currently on an epidural 
(at each refresh looks back and collect all the current epidural flowsheets)
Calculate the current number of patients who have had epidural volume 7001026  documented in the last four hours 
Present this number on the front tile as 'number of patients on epidural'. 

*Note Average time between motorblock assessments - suggest not on front tile- TBC.* 


## [B] Floorplan labelling 

## PATIENTS WHO ARE ON EPIDURAL FLOOR PLAN

ELIGIBILITY

All patients

**Whether a patient is on an epidural for their pain management should be denoted on the existing pain score floor plan** 

1. If data entered in flowsheet 7001026 in the last 12 hours, label patient as 'on epidural'. ?Icon or letter 'E' in Bed. 
2. If none of the epidural drug flowsheets have been documented in the last 12 hours, the patient is not on an epidural. No change. 

## MOTOR BLOCK ASSESSMENT FLOOR PLAN

All patients who have been on an epidural in the last four hours need to have their level of motor block, also called the Bromage Score assessed 2 hourly in day and 4 hourly in the day. 
There will be an additional floorplan button added to the pain floor plan entitled 'Motor Block Assessment'

ELIGIBILITY

All patients on an epidural

*Patients with epidurals to be visualy highlighted. Others are not included in the calculation*

## Primary Label Assessment of Motor Block/Bromage Score Label 

1. If either the latest 'Assessment of Motor Block Lt leg' or 'Assessment of Motor Block Rt leg assessment' entry is  0 or 1, label patient as 'bromage score = 0 or 1'; GREEN
2. If either the latest 'Assessment of Motor Block Lt leg' or 'Assessment of Motor Block Rt leg assessment' entry is 2, label patient as 'bromage score = 2'; AMBER
3. If either the latest 'Assessment of Motor Block Lt leg' or 'Assessment of Motor Block Rt leg assessment' entry is 3, label patient as 'bromage score = 3'; RED


## Secondary Label Assessment of Motor Block/Bromage Score label-
*In addition to the last documented Motor Block Assessment, we need to display whether a motor block assessment is overdue*

1. If there has never been an 'Assessment of Motor Block Lt leg' or 'Assessment of Motor Block Rt leg assessment' since the patients has been classified as 'on epidural', then label patient as 'missing assessment'. Red Hashed and no fill bed.  
2. If the current time is 08:00-19:59, if either 'Assessment of Motor Block Lt leg' or 'Assessment of Motor Block Rt leg assessment' have not been completed in the last two hours, then label patient as 'missing' and forward fill the latest motor block asessmeent reading. 
Bed to be red hashed outline (with fill of colour from forward filled entry). 
3. If the current time is 20:00-07:59, if either 'Assessment of Motor Block Lt leg' or 'Assessment of Motor Block Rt leg assessment' have not been completed in the last four hours, then label patient as 'missing' and forward fill the latest motor block asessmeent reading. 
Bed to be red hashed outline  (with fill of colour from forward filled entry).
_______________________________________________


DRAFT below- 

[D] SPC CHARTS

Operational definition - For patients on epidurals, what percentage of motor block assessements are done on time as per guidelines. Chart a- day, Char b- night. 

Measurement Interval (for motor block assessment scoring only)
Average time between motorblock assessments - note suggest not on front tile- TBC. 

ABC SPC CHARTS (refer to XYZ metric in classification

Calendar day defined as 00:00 - 23:59
Week defined as Monday 00:00 – Sunday 23:59


These are weekly percentage (p-charts) SPC
Week defined a Monday 00:00 – Sunday 23:59
