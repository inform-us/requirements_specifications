# Capturing INFORM patient data for a critical care admission

## Overview

**Data is caputured at four points:**
- FRONT TILE unit metric; summary data looking back 24 hours including patients present within that time window and those that have been discharged
- FLOOR PLAN; individual current patient / bed space data
- INDIVIDUAL PATIENT GRAPH; data looking back up to 72 hours for the individual patient
- SPC chart; summary data for one week (see individual metrics for respective definitions) including all patients still present and thos discharged within that time window

**In order for these data to be processed for the above metrics a longer time time window needs to be sampled to account for:**
- ELIGIBILITY; an additional 6 hours of data to determine whether an individual is eligible for that metric calculation (e.g. is receivng oxygen or is receiving vasoactive drugs)
- ALL_TARGET SET metric is calculated differently; taking a single daily snapshot at 13:00 (code actually set to do this calcaultion at 13:30 to give some clinical leeway) of current inpatients (ie. does not include those that have been discharged, but would include those that are temporalily off the unit (see below) and as such that calcualtion would need amending). In order to fulfil this metric at all times an additional 5 hours of data is required. 
- METRIC COMPLIANCE TO SET TARGET; doctors set new targets (i) on admission, (ii) clinical change or during the morning ward rounds 08:00 - 13:00. For the puposes of the ALL_TARGETS METRIC, targets are reset at 07:59 (ie. become invalid) allowing new targets to be set form 08:00. However, during this period where new targets are set (08:00 - 13:00), complicance of physiological metric to targets still needs to take place. As such the logic allows for a previous target (set anytime bewteen 08:00 on the previous day and 07:59 on the current day to 'roll-over' until 12:00 on the current day, for the purposes of compliance calculation ONLY for the following: SpO2, MAP, & RASS. In order to fulfil this metric at all times an additional 5 hours of data is required. **BUT SPC WOULD NEED MORE** [NEED to check but 16 for a week that starts on calendar day and up to 24 for 'shift' week]
- BACKFILLING; ICU observation frequencies are not usually <4 hourly, most physiological metrics are charted between 1-4 hourly, but the logic allows for a 15 minute 'clinical leeway' in charting. In order to allow backfilling an additional 5 hours of data is required.
- TIME OFF ICU vs. MISSING; (i) data collected while off the ICU should not be included in analysis (even if the patinet returns to the ICU as part of the same admission (e.g. away for CT scan); (ii) however this time off the unit has to be recorded and displayed on the INDIVIDUAL PATIENT GRAPH, both to differentiate it form 'missing data' and to avoid a collapsed time-line on the x-axis
**QUESTION - how can we label as off unit unless they have returend back to the unit?**

## Patient Flow and 

- a critical care admission may form part of a patient's hospital visit
- a critical care admission is characterised by a time period in a specified ICU bed location
- patients may move to another ICU bed location within the same critical care admission
- patients may leave the ICU to another location (within the hospital, including another ICU or be dicharged form the hospital) 
- patients may die, ending their critical care admission (leaving their specified ICU bed location)
- patients may move off the unit and return within the same critical care admission
- these rules seek to determine how to:
1. Handle flow sheet data while 'off' the ICU
2. Differentiate a discharge, from a bed move (within the same ICU), from a readmission (to the same ICU), from a period 'off' the ICU for an investigation / procedure

## Patient flow & Data Items used to determine admission / dicharge / 'off ICU'

Patients may move between multiple locations as part of one hospital visit.

For the pusposes of INFORM, we do not seek the admission location prior to a critical care admission. 
Patients may be admitted form anywhere within the hospital or from outside the hospital (ie. another hospital or home). 

XXX
Once in critical care they may be moved during a defined admission, potentially multiple times:
- moved to a different bed in the same unit
- moved for surgery/procedure/imaging and comes back to the same bed
- moved for surgery/procedure/imaging and comes back to a different bed

Or moved (away from this unit), again potentially multiple times:
- another ICU at UCH
- another ICU elsewhere
- ward
- home
- died
- another hospital

## Representing patient flow in EMAP / UDS

Patient movements are captured in three different tables in `uds.star`: `hospital_visit`, `location_visit` and `location`. 
- `hospital_visit`: each row represents an entire hospital stay for a single patient. This may involve moving between multiple different locations within the hospital.
  
- `location_visit`: each row represents a stay at a certain hospital location (e.g. a specific bed in a specific unit) for a single patient. The location is given by a `location_id` which corresponds to a row in the `location` table. 
  
- `location`: lists every possible location inside the hospital, along with its hl7 string e.g. `T03^T03 BY01^BY01-11`.

Patient movements are represented as follows:

### Initial admission to hospital:
- Creates a `hospital_visit` row with a specific admission datetime + a discharge datetime of `NULL`.
  
- Creates a `location_visit` row with a specific admission datetime + a discharge datetime of `NULL`. Its `location_id` corresponds to the bed the patient is admitted to.

### Moved to another bed in the unit:
- The discharge datetime of their current `location_visit` row is set to the movement time.
  
- A new `location_visit` row is created with an admission datetime of the movement time + a discharge datetime of `NULL`. Its `location_id` matches the new bed location.
  
- If the patient is moved multiple times within the same unit, then they will have one `location_visit` row for each bed location they have occupied.

### Moved away from the unit (to another ward / operating theatre etc.):
- Same as above (for moved to another bed in the unit), except the `location_id` will now correspond to a location outside of the unit.
  
- Each time they are moved out of the unit, or to any other location in the hospital, this will generate a new `location_visit` row for each location they have occupied.

- If they return to the unit, this will be handled in the same way, by creation of a new `location_visit` row with a location id corresponding to a bed in the unit.

### Discharged from hospital:
- The discharge datetime of their `hospital_visit` row is set to the discharge time.
- The discharge datetime of their current `location_visit` row is set to the discharge time.

### Died in hospital:
- The `date_of_death` and `datetime_of_death` in `uds.star` `core_demographic` will be set for this patient.
  
- In most cases, this should also set their `hospital_visit` discharge datetime and `location_visit` discharge datetime. In rare cases, the `hospital_visit` discharge datetime and/or `location_visit` discharge datetime may remain as `NULL`.

## Handling moved / discharged patients

### T03 'wait' bed

On T03 there is a 'wait' bed denoted by `T03^T03 WAITING^WAIT`. This 'wait' bed isn't used consistently, so it is unclear what it represents exactly. 

All data from the 'wait' bed should be excluded from all informus data.

### 'ghost' patients

'ghost' patients appear as rows with a `NULL` `hospital_visit` admission datetime. All data from 'ghost' patients (i.e. hospital visits with a `NULL` admission) should be excluded from all informus data.

### Tiles (i.e. `unit_wide` data)

All tiles should include data from any patient that has been on the unit in the last 24 hours including: 

- patients that have since been moved to another location in the hospital
  
- patients that have since been discharged from the hospital and/or died
  
The exceptions to this are: `bed occupancy` and `all targets set` - these tiles should only use data from patients currently present on the unit.

For those that include discharged/moved patients, they should use all data produced by patients _on the current unit_ in the last 24 hours. For example, let's consider the tiles on the T03 dashboard. Let's imagine a patient has been on T03 for multiple days in a specific bed, before being moved 12 hours ago to another ward. In this scenario we would use all data generated by the patient on T03 in the last 24 hours (so from 12-24 hours ago), but ignore any data generated while they are off the unit (0-12 hours ago). No data generated outside of the unit should be included in any tile calculations.

This also holds true for shorter trips in and out of the unit. For example, let's imagine a patient has been on T03 for multiple days in a specific bed, before being moved 12 hours ago to another location in the hospital (could be another ward, or the operating theatre, imaging etc.), before being transferred back to a bed on T03 10 hours ago (this could be the same bed as before or a different one). In this scenario we would use all data generated by the patient on T03 in the last 24 hours (so 0-10 hours ago, as well as 12-24 hours ago), but ignore any data generated during the 2 hours they were off the unit.

Equally, we must ensure that any data 'gaps' in the last 24 hours (due to the patient being outside the unit, in another location in the hospital), don't negatively impact the scores on each tile. There is no data for these patients on T03 in these gaps, so they shouldn't contribute to the overall score.

Tiles should still show data if there are no patients currently on the unit (as long as there have been some moved / discharged patients present in the last 24 hours). Clicking on a tile for any metric should show an empty floorplan in this scenario (i.e. every bed shows an `empty` status).

If there are no current patients and there haven't been any in the last 24 hours, then no tiles should be displayed and instead a message should be shown that reads 'There have been no patients on this unit in the last 24 hours'.

The time window is always exactly 24 hours (even over a daylight savings transition).

### Floorplan (i.e. `latest` data)

The floorplan (i.e. the view with beds as individual coloured rectangles), should only include data for patients currently on the unit (i.e. patients that have since been discharged or moved to another location in the hospital should be excluded). 

As above, we still need to ensure that we only use data generated within the current unit, excluding any that may have been generated while the patient was in another location in the hospital. Bear in mind that current patients may have previously been moved in/out of the unit, as well as within the unit within our time period of interest. 

### Metric charts (i.e. `24hr` / `72hr` data)

The metric charts (shown when clicking on a bed in the floorplan), should only include data for patients currently on the unit (i.e. patients that have since been discharged or moved to another location in the hospital should be excluded). 

As above, we still need to ensure that we only use data generated within the current unit, excluding any that may have been generated while the patient was in another location in the hospital. Times when the patient was off the unit will appear as 'missing' data in the chart.

### SPC charts

The SPC charts should include data from all patients that have been on the unit in the relevant time period. As above, we still need to ensure that we only use data generated within the unit, excluding any that may have been generated while patients were in other locations in the hospital. 

As with the tiles, we must ensure that any data 'gaps' (due to patients being outside the unit, in another location in the hospital), don't negatively impact the scores for that week. For example, say a patient was on T03 on Monday, before being transferred to another unit for most of the week and transferred back to T03 for the last hour of Sunday. The fact that most of their data is 'missing' for that week (due to being off the unit) shouldn't negatively impact the overall scores.
