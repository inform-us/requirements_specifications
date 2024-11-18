# Moved and discharged patients

## Patient flow

Patients may move between multiple locations as part of one hospital visit.

First, they are admitted to one of the following locations:
- emergency department
- ward
- theatres / radiology / procedure suite
- outpatients
- an external hospital
- others

Then they may be moved (staying in same unit), potentially multiple times:
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

Patient movements are captured in two different tables in `uds.star`: `hospital_visit` and `location_visit`. 
- `hospital_visit`: each row represents an entire hospital stay for a single patient. This may involve moving between multiple different locations within the hospital.
  
- `location_visit`: each row represents a stay at a certain hospital location (e.g. a specific bed in a specific unit) for a single patient. The location is given by a `location_id` which corresponds to a row in the `uds.star` `location` table. Each 'location visit' is associated with a specific 'hospital_visit'.

Patient movements are represented as follows:

- Initial admission to hospital:
  - This creates a `hospital_visit` row with a specific admission datetime + a discharge datetime of `NULL`.
  - This creates a `location_visit` row with a specific admission datetime + a discharge datetime of `NULL`. Its `location_id` corresponds to the bed the patient is admitted to.

- Moved to another bed in the unit:
  - The discharge datetime of their current `location_visit` row is set to the movement time.
  - A new `location_visit` row is created with an admission datetime of the movement time + a discharge datetime of `NULL`. Its `location_id` matches the new bed location.
  - If the patient is moved multiple times within the same unit, then they will have one `location_visit` row for each bed location they have occupied.

- Moved for surgery / procedure / imaging + returned to same bed (**TODO - to be checked**):
  - This results in no changes to the `location_visit` or `hospital_visit` tables. Surgery / procedure / imaging aren't recorded as new 'locations' so the patient will still appear to be on the unit they were moved from.

- Moved for surgery / procedure / imaging + returned to a different bed (**TODO - to be checked**):
  - The discharge datetime of their current `location_visit` row is set to the movement time?
  - A new `location_visit` row is created with an admission datetime matching when the patient was returned to unit + a discharge datetime of `NULL`. Its `location_id` matches the new bed location.

- Moved to another location in the hospital (e.g. another ward / another ICU at UCH):
  - The discharge datetime of their current `location_visit` row is set to the movement time.
  - A new `location_visit` row is created with an admission datetime of the movement time + a discharge datetime of `NULL`. Its `location_id` will refer to the new location.

- Discharged from hospital:
  - The discharge datetime of their `hospital_visit` row is set to the discharge time.
  - The discharge datetime of their current `location_visit` row is set to the discharge time.

- Died in hospital:
  - Same as 'discharged from hospital' (above), but the `date_of_death` and `datetime_of_death` in `uds.star` `core_demographic` will be set for the patient also.

## Handling moved / discharged patients

### Handling moved patients for a specific unit

If a patient is moved into the unit from another location in the hospital, this should be treated as a new admission i.e. any data generated prior to moving into the current unit is ignored. Note: this includes data generated in other hospital locations, as well as any prior data the patient may have on that unit. Only data since their latest move into the unit is considered.

This scenario will appear in the data as multiple `location_visit` rows. At least one row will have a `location_id` outside the current unit, followed by a row with one inside the unit.

The same applies when the patient is moved out of the unit (to another location in the hospital). Any data generated after that point (in any location) is ignored.

If a patient is moved inside of the same unit, then this should be treated as the same admission i.e. all data is retained. This scenario will appear as multiple consecutive `location_visit` rows with `location_id`s from the unit. These should be summarised to one row with the latest `location_id` in the unit and the earliest `admission_datetime` from their current visit to the unit. (bear in mind they may have visited the unit previously, before being transferred to another location and back again. We only summarise the rows from the latest visit)

### T03 'wait' bed

On T03 there is a 'wait' bed denoted by `T03^T03 WAITING^WAIT`. This 'wait' bed isn't used consistently, so it is unclear what it represents exactly. 

All data from the 'wait' bed should be excluded from all informus data.

### Tiles (i.e. `unit_wide` data)

All tiles should include data from any patient that has been on the unit in the last 24 hours including: 
    - patients that have since been moved to another location in the hospital
    - patients that have since been discharged from the hospital and/or died
The exceptions to this are: `bed occupancy` and `all targets set` - these tiles should only use data from patients currently present on the unit.

Tiles should still show data if there are no patients currently on the unit (as long as there have been some moved / discharged patients present in the last 24 hours). Clicking on a tile should show an empty floorplan in this scenario.

If there are no current patients and there haven't been any in the last 24 hours, then tiles should display text that says 'no data available'.

The time window is always exactly 24 hours (even over a daylight savings transition).

### Floorplan (i.e. `latest` data)

The floorplan (i.e. the view with beds as individual coloured rectangles), should only include data for patients currently on the unit. Bear in mind though, that a current patient may have previously been moved one (or multiple) times within the same unit, so you will still need to summarise this to one row.

### Metric charts (i.e. `24hr` / `72hr` data)

The metric charts (shown when clicking on a bed in the floorplan), should only include data for patients currently on the unit.

### SPC data

This should include data from all patients that have been on the unit.

## Moved patients explanation

- These are patients who have a date value in `location_visit_discharge_dt` but DO NOT have a value in `hospital_visit_discharge_dt`
- Moved patients fall under one of the following circumstances:
    - Patients who were in a bed at one point in time, but have now moved to a different bed on the same unit
        - Potentially produces a duplicated data row returned from our patients query (i.e. multiple rows of the same bed). This is because the data contains the moved patient who used to be in that bed as well as the new patient who is now currently occupying that same bed.
        - One of the rows will have a date value in the `location_visit_discharge_dt` column, the other row will have `null` for that column
    - Patients who are readmitted to the same bed, for instance if they were temporarily moved for surgery and then came back to the same bed
        - Produces a duplicated data row returned from our patients query
        - One of the rows will have a date value in the `location_visit_discharge_dt` column, the other row will have `null` for that column
    - Patients who are currently away for surgery (or possibly moved to a different unit)
        - Produces one data row in our patients query, because the patient hasn’t come back yet (i.e. there is no duplicated row yet)
        - But they might come back at some point, at which point we would have a duplicate data row returned from our patients query

## Discharged patients explanation

- These patients have a date value in both `location_visit_discharge_dt` AND `hospital_visit_discharge_dt`
- Discharged patients fall under the following circumstance:
    - Patients who have been completely discharged from the hospital
        - They won’t have a duplicate row returned from our patients query because they are now discharged from the hospital and are not currently occupying a bed

## How to handle moved patients

- Patients who were in a bed at one point in time, but have now moved to a different bed on the same unit
    - Treat the duplicated patient row that does not have a `location_visit_discharge_dt` as the valid data point (because this is where the patient was moved to),
    - Replace the `admission_dt` of the chosen valid data point with the earlier `admission_dt` of the old duplicated data point. We do this as we want to retain their original `admission_dt`
    - Discard the old and no longer needed duplicated data point
    - The remaining valid data point should be considered as a `current` patient and included in both our `unit_wide` statistics AND occupy a bed on the frontend
- Patients who are readmitted to the same bed, for instance if they were temporarily moved for surgery and then came back to the same bed
    - Same solution as above
- Patients who are transferred out of ICU (either to a non-ICU ward, or another hospital, or gone home)
    - These patients should be included in our `unit_wide` calculations, but not as part of our current patients list
    - They should not appear as an occupied bed on the frontend

## How to handle discharged patients

- They should be included in our `unit_wide` statistics,
- They should not be included in our list of `current` patients and should not appear as an occupied bed on the frontend
