# Moved and discharged patients

The `recent_patients.sql` currently returns all patients including `current` , `moved` , and `discharged` patients all in the same query. Then we have further python logic to parse them all out. The discharged patients are not currently saved to mongodb, but we need to implement this so that they can be picked up on the frontend. There might also be some additional edge cases that we haven’t yet covered.

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

PATIENT FLOW

Admission:
- emergency department
- ward
- theatres / radiology / procedure suite
- outpatients
- an external hospital
- others

Moved - stay in same unit:
- moved to different bedspace
- moved to for surgery/procedure/imaging and comes back to same bed space
- moved to for surgery/procedure/imaging and comes back to different bed space

Moved - away from this unit:
- another ICU
- ward
- home
- died
- another hospital
