# Capturing INFORM patient data for a critical care admission

## Overview

## Patient flow through the hospital 

INFORMus collects data from critical care admissions i.e. time periods spent in [specified ICU bed locations](#icu-bed-locations). A patient may not stay in the same bed location for their entire hospital visit (associated with a single csn). For example:

- patients may move to another bed location in the same ICU

- patients may leave the ICU to another location within the hospital (including another ICU, or another ward)

- patients may temporarily move off the ICU for surgery / procedure / imaging and then return (either to the same bed location or a new one).

- patients may be discharged from the hospital

- patients may die, ending their critical care admission (leaving their specified ICU bed location)

These rules seek to determine:

- which patients to consider for each part of INFORM (e.g. tiles, floorplans and charts) 
  
- How to differentiate a bed move (within the same ICU) from a move outside the ICU (either temporarily for an investigation/procedure or permanently to another ward)
  
- How to handle flowsheet data produced in another location in the hospital ('off' the current ICU)
  
- How to exclude time 'off' the current ICU from tile statistics and SPC data

## ICU bed locations

INFORM collects data from patients in all bed locations within `T03`, `T06`, `GWB` and `WMS`, with a few exceptions (see below). For the purposes of INFORM, we do not seek the admission location prior to a critical care admission. Patients may be admitted from anywhere within the hospital or from outside the hospital (ie. another hospital or home). 

### T03 'wait' bed

On T03 there is a 'wait' bed denoted by `T03^T03 WAITING^WAIT`. This 'wait' bed isn't used consistently, so it is unclear what it represents exactly. All data from the 'wait' bed should be excluded from all informus data.

### Additional T06 beds

T06 has two additional beds represented by `?` and `?` that are functional, but not currently used. All data from these beds should be excluded from all informus data.

(TODO - there are a number of beds listed in the star location table for T06 we don't use:
- `1020100171^T06PACU WAITING^WAIT`
- `1020100171^T06PACU SR39^SR39-39`
- `1020100171^T06PACU BY09^BY09-40`
- `1020100171^T06PACU BY09^BY09-41`
- `1020100171^T06PACU BY11^BY11-50`
- `1020100171^T06PACU BY12^BY12-52`
- `1020100171^T06PACU BY07^BY07-32`
- `1020100171^T06PACU BY07^BY07-33`
- `1020100171^T06PACU BY07^BY07-35`
- `1020100171^T06PACU BY08^BY08-36`
- `1020100171^T06PACU BY08^BY08-38`
- `1020100171^T06PACU BY08^BY08-37`
Are any of these relevant?
)

(TODO - WMS also seems to have a wait bed `WSCC^WMSCCU WAITING^WAIT` - should we mention this?)

### 'ghost' patients

For all bed locations, we exclude any data from 'ghost' patients. These are patients with a `NULL` `hospital_visit` admission datetime. None of their data should be included in any part of INFORM.

## Patient data is captured at four points in INFORM

- [FRONT TILE unit metric](#tiles-ie-unit_wide-data)  
  Summary data looking back 24 hours including all patients that were present **at any point** within that time window (i.e. patients currently on the unit now + patients that were on the unit in the last 24 hours that have since been moved to another location in the hospital or discharged). Note: some tiles have exceptions to this (see below)
  
- [FLOOR PLAN](#floorplan-ie-latest-data)  
  Individual current patient / bed space data.
  
- [INDIVIDUAL PATIENT GRAPH](#metric-charts-ie-72hr-data)   
  Data looking back up to 72 hours for the individual current patients
  
- [SPC chart](#spc-charts)  
  Summary data for one week (see individual metrics for respective definitions) including all patients present **at any point** within that time window. This includes patients that were present for the entire week, as well as those that were present for only part of the week, before being moved to another location in the hospital or discharged.

For all parts of INFORM, we should only include data produced by patients on the current unit of interest (i.e. exclude any flowsheet readings produced in other locations in the hospital). Airway is the only exception, where flowsheets from all units are valid with no time validity limit (see [the airway rules](./Airway%20Plan.md)). As such airway is an exception to all the specific on/off unit rules provided below.

## Tiles (i.e. `unit_wide` data)

All tiles should include data from any patient that has been on the unit in the last 24 hours including: 

- patients that have since been moved to another location in the hospital
  
- patients that have since been discharged from the hospital and/or died
  
The exceptions to this are: `bed occupancy`, `all targets set` and `Airway Plan` - these tiles should only use data from patients currently present on the unit.

### Only use data collected on the current unit

For tiles that include discharged/moved patients, they should use all data produced by patients _on the current unit_ in the last 24 hours. For example, let's consider the tiles on the T03 dashboard. Let's imagine a patient has been on T03 for multiple days in a specific bed, before being moved 12 hours ago to another ward. In this scenario we would use all data generated by the patient on T03 in the last 24 hours (so from 12-24 hours ago), but ignore any data generated while they are off the unit (0-12 hours ago). No data generated outside of the unit should be included in any tile calculations.

This also holds true for shorter trips in and out of the unit. For example, let's imagine a patient has been on T03 for multiple days in a specific bed, before being moved 12 hours ago to another location in the hospital (could be another ward, or the operating theatre, imaging etc.), before being transferred back to a bed on T03 10 hours ago (this could be the same bed as before or a different one). In this scenario we would use all data generated by the patient on T03 in the last 24 hours (so 0-10 hours ago, as well as 12-24 hours ago), but ignore any data generated during the 2 hours they were off the unit.

Note: during processing, you will need to consider a larger time window for most metrics to ensure calculated statistics are correct (see [extended hours](#extended-time-window-for-metric-processing)).

### Exclude off unit hours from statistics

Time off the unit (for any reason e.g. before admission to hospital, after discharge from hospital, transfer to another ward/ICU, temporary movement for surgery...) should be excluded from all tile statistics. For example:

#### Tile percentages / total hours

For metrics with tile percentages or 'total hours' (such as Sedation RASS, Blood Oxygen Saturation (SPO2), Mean Arterial Blood Pressure (MAP) etc.), off unit time should be excluded. Any hourly epochs when a patient isn't on the unit at any time during that hour should be excluded from the denominator of the percentages (%) and from the displayed 'total hours' e.g. 'total hours on... sedation, oxygen therapy, mandatory ventilation, vasoactive drugs'.

This ensures that e.g. a patient being transferred off the unit temporarily for a long surgery doesn't negatively impact scores like the % of readings on target. It's impossible to take observations during their time off unit, so that time shouldn't contribute to their overall score.

#### Pain/ RASS average time between measurements

For these metrics, we calculate an average time between measurements for the tile (i.e. we take pairs of sequential readings, calculate the time interval between them and take an average). Any interval that includes an hour or more off unit time should be excluded. This is because if a patient is off the unit for a long period of time, e.g. for an operation, this would greatly skew the mean time between measurements even though taking observations at these times is impossible.

For example, say a patient was present in a bed on T03, before being moved for surgery for 4 hours, and then returning to the same bed on T03. We would calculate intervals between all sequential pairs of pain readings taken on T03, excluding the one between the last reading before they were moved for surgery and the first one after they returned. This would remove the long interval of > 4 hours, which was caused by their movement off the unit.

### Tile display

Tiles should still show data if there are no patients currently on the unit (as long as there have been some moved / discharged patients present in the last 24 hours). Clicking on a tile for any metric should show an empty floorplan in this scenario (i.e. every bed shows an `empty` status).

If there are no current patients and there haven't been any in the last 24 hours, then no tiles should be displayed and instead a message should be shown that reads 'There have been no patients on this unit in the last 24 hours'.

The time window is always exactly 24 hours (even over a daylight savings transition).

## Floorplan (i.e. `latest` data)

The floorplan (i.e. the view with beds as individual coloured rectangles), should only include data for patients currently on the unit (i.e. patients that have since been discharged or moved to another location in the hospital should be excluded). 

As above, we still need to ensure that we only use data generated within the current unit, excluding any that may have been generated while the patient was in another location in the hospital. Bear in mind that current patients may have previously been moved in/out of the unit, as well as within the unit within our time period of interest.

#### SPO2, Mean Arterial Blood Pressure and Tidal Volume metrics

Note these metrics classify patients for the floorplans according to summative rules and not real-time status of whether they are above, below or in range of target... e.g. 'Tidal volumes are above 8 mL/kg IBW for 3 consecutive hours OR 5 non-consecutive hours within the preceding 24 hours; OR tidal volumes are above 10 mL/kg IBW for 2 consecutive hours'. We therefore need individual rules to handle any 'off unit' hours (to be solved with https://github.com/inform-us/INFORMus/issues/1756) - see the 'labelling rules' for the individual metrics.

### Metric charts (i.e. `72hr` data)

The metric charts (shown when clicking on a bed in the floorplan), should only include data for patients currently on the unit (i.e. patients that have since been discharged or moved to another location in the hospital should be excluded). 

As above, we still need to ensure that we only use data generated within the current unit, excluding any that may have been generated while the patient was in another location in the hospital. Times when the patient was off the unit should be marked with a different colour on the chart.

### SPC charts

The SPC charts should include data from all patients that have been on the unit in the relevant week. This includes patients that were present for the entire week, as well as those that were present for only part of the week, before being moved to another location in the hospital or discharged. As above, we still need to ensure that we only use data generated within the unit, excluding any that may have been generated while patients were in other locations in the hospital. 

As with the tiles, we must ensure that off unit time is excluded from any statistics. The same rules apply for removing off unit time from the denominator of percentages (%) and for excluding intervals with an hour or more off unit time (for pain + rass assessment frequency).

## Extended time window for metric processing

While each of the features above considers a specific time window (e.g. 24 hours for metric tiles, or 72 hours for patient graphs), a larger time window must be sampled to ensure calculated statistics are correct (see below). Currently, an extra 30 hours of data is included, which is large enough to cover the requirements for all metrics. These extra hours should be included during processing, but removed from the final result. For example, for the patient graphs, 72 + 30 hours of data are used during processing (102 hours), but only 72 hours of results are returned. As with the examples above, only data generated on the current unit should be considered, excluding any that may have been generated while patients were in other locations in the hospital. 

Note: there are some exceptions to this for specific metrics (for example, airway). See the rules for the individual metrics.

Some of the factors that require this longer time window:

- ELIGIBILITY; an additional 6 hours of data to determine whether an individual is eligible for that metric calculation (e.g. is receiving oxygen or is receiving vasoactive drugs)

(TODO - currently the all_target set tile will only include patients present on the unit right now. i.e. if a patient is away from the unit temporarily for surgery etc. (but this shows up as a location visit discharge) they won't be included - is this fine?)
- ALL_TARGET SET metric is calculated differently; taking a single daily snapshot at 13:00 (code actually set to do this calculation at 13:30 to give some clinical leeway) of current inpatients (ie. does not include those that have been discharged, but would include those that are temporarily off the unit (see below) and as such that calculation would need amending). In order to fulfil this metric at all times an additional 5 hours of data is required. 
  
- METRIC COMPLIANCE TO SET TARGET; doctors set new targets (i) on admission to the unit, (ii) clinical change or during the morning ward rounds 08:00 - 13:00. For the purposes of the ALL_TARGETS METRIC, targets are reset at 07:59 (ie. become invalid) allowing new targets to be set form 08:00. However, during this period where new targets are set (08:00 - 13:00), compliance of physiological metric to targets still needs to take place. As such the logic allows for a previous target (set anytime between 08:00 on the previous day and 07:59 on the current day) to 'roll-over' until 12:00 on the current day, for the purposes of compliance calculation ONLY for the following: SpO2, MAP, & RASS. In order to fulfil this metric at all times an additional 5 hours of data is required. **BUT SPC WOULD NEED MORE** [NEED to check but 16 for a week that starts on calendar day and up to 24 for 'shift' week]
  
- BACKFILLING; ICU observation frequencies are not usually <4 hourly, most physiological metrics are charted between 1-4 hourly, but the logic allows for a 15 minute 'clinical leeway' in charting. In order to allow backfilling an additional 5 hours of data is required.

## Representing patient flow in EMAP / UDS

This section provides an overview of the technical details of how patient movements are stored in the EMAP/UDS databases.

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

- Note: some temporary movements off the unit may not be represented in EMAP/UDS. For example, we have observed that some temporary movements (e.g. for imaging like endoscopy / MRI..) followed by return to the same bed do not produce a new `location_visit` row, while others do (e.g. movement to an operating theatre). Movements that don't produce a new `location_visit` row can't be detected and, as such, those patients will be treated as if they were present in the same bed in the unit the entire time. 

### Discharged from hospital:
- The discharge datetime of their `hospital_visit` row is set to the discharge time.
  
- The discharge datetime of their current `location_visit` row is set to the discharge time. Note that in rare cases, the `location_visit` discharge datetime may remain as `NULL`.

### Died in hospital:
- The `date_of_death` and `datetime_of_death` in `uds.star` `core_demographic` will be set for this patient.
  
- In most cases, this should also set their `hospital_visit` discharge datetime and `location_visit` discharge datetime. In rare cases, the `hospital_visit` discharge datetime and/or `location_visit` discharge datetime may remain as `NULL`.
