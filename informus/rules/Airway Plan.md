Some chagnes to review here

# Airway Plan 
Rules for the Airway Plan [completed] Metric


## EPIC
- the ICU Airway Plan is completed by doctors
- it is accessed in ICU Navigators - Airway and Turning [doctors' log in view]
- in addition, if an 'Airway Alert' exists (left hand side of EPIC screen with allergies and other alerts), clicking on it will also take you to the ICU Airway Plan
- the medical team should complete the ICU Airway Plan on admission to critical care, following assessment of any new upper airway pathology and after any procedure involving the airway (e.g. re-intubation, tracheostomy, bronchoscopy, difficult nasogastric tube insertion, SL&T review etc)
- some of above review triggers are either more nuanced (subtle clinical changes) or rely on free text entry in EPIC - these will not be considered
- other review triggers are more certain and are documented in EPIC flowsheets (e.g new endotracheal tube insertion or tracheostomy insertion)
- there is currently no concensus on whether an ICU Airway Plan should also be subject to a review date (cf 24 hours for ICU targets), separate to the triggers mentioned above
- the most favoured opinion is a 7-14 day validity, with the bulk of the reviews falling on longer stay patients who are more likely to have a less dynamic airway 
- ICU Airway Plan is a binary metric (an airway plan is either completed or not completed)


## EPIC Flowsheets <br>

**Components of the ICU Airway Plan**
ICU Airway Plan - Group ID G UCLH ICU AIRWAY PLAN [23864]

| Flowsheet | Row ID | Manual / Automatic / Calculated Input | Comments | Expected documentation frequency |
|-|-|-|-|-|
| Airway | R UCLH ICU AIRWAY PLAN 24499 | Manual | Options: <br> - Natural Airway <br> - Endotracheal Tube <br> - Percutaneous Tracheostomy <br> - Surgical Tracheostomy <br> - Laryngectomy <br> - Other (free text) | On completion of airway plan |
| DAS Generic Airway Plan | R UCLH ICU AIRWAY PLAN DAS 24498 | Manual | Options: <br> - Yes <br> - No <br> - Other (free text) | On completion of airway plan |
| Plan A | R UCLH ICU AIRWAY PLAN A 23865 | Manual | Free text | On completion of airway plan (if DAS Generic Airway Plan = No) |
| Emergency Teams | R UCLH ICU AIRWAY PLAN TRACHE CALL 24504 | Manual | Options: <br> - Anaesthesia <br> - ICU <br> - ENT <br> MaxFax <br> - DART <br> - Other (free text) | On completion of airway plan |

**Components of the ICU Turning Plan**
ICU Turning Plan - Group ID G UCLH ICU TURNING PLAN [24505]

| Flowsheet | Row ID | Manual / Automatic / Calculated Input | Comments | Expected documentation frequency |
|-|-|-|-|-|
| Doctor Required | R UCLH ICU TURNING PLAN DOC REQ 24508 | Manual | Options: <br> - Yes <br> - No <br> - Other (free text) | Optional on completion of airway plan |
| Senior Nurse Required | R UCLH ICU TURNING PLAN NURSE REQ 24509 | Manual | Options: <br> - Yes <br> - No <br> - Other (free text) | Optional on completion of airway plan |

**Associated flowsheet_IDs used in this metric**
Respiratory Observations - Group ID G UCLH ICU RESPIRATORY OBS FOR ASSESSMENT [40722]

| Flowsheet | Row ID | Manual / Automatic / Calculated Input | Comments | Expected documentation frequency|
|-|-|-|-|-|
| O2 delivery device |R OXYGEN DELIVERY METHOD 3040109305 | Drop down (free text available) |Select drop down options: <br> - Nasal cannula <br> - Simple mask <br> - Venturi mask <br> - Capno mask <br> - High-flow nasal cannula (HFNC) <br> - Humidified oxygen mask <br> - Non-rebreather mask <br> - Tracheostomy mask <br> - CPAP/Bi-PAP mask <br> - Oxyhood <br> - Bag valve mask (BVM) <br> - Endotracheal tube <br> - Tracheostomy <br> - Other (comment) <br> - No respiratory support provided | Hourly (varies depending on patient's clinical condition)|

ETT Properties Row ID 3040102626 links to LDA AVATAR - Placement Date Row ID 700 - Placement Time Row ID 701 <br>
Surgical Airway Properties Row ID 700004 links to LDA AVATAR - Placement Date Row ID 700 - Placement Time Row ID 701

## Eligibility
All patients across all units 


## Validity (time window) Rules: 

- all patients should have an ICU Airway Plan documented during an admission to critical care
- an ICU Airway Plan is only deemed COMPLETED if option A OR option B is met

**Option A** <br>
- Airway [Row ID 24499] completed - this will return one of the following options: Natural Airway / Endotracheal Tube / Percutaneous Tracheostomy / Surgical Tracheostomy / Laryngectomy / Other and have a _dt stamp

- AND DAS Generic Airway Plan [Row ID 24498] = YES and has a dt stamp
- DAS Generic Airway Plan [Row ID 24498] = NO or OTHER or there is no data entered, Option A is not satisfied.

**Option B** <br>
- Airway [Row ID 24499] completed - this will return one of the following options: Natural Airway / Endotracheal Tube / Percutaneous Tracheostomy / Surgical Tracheostomy / Laryngectomy / Other and have a _dt stamp
- AND DAS Generic Airway Plan [Row ID 24498] = NO or 'other' and has a dt stamp or there is no data entered

- PLUS Plan A [Row ID 23865] - any entry generating a _dt stamp

**Validity** <br>
- as there is currently no consensus on whether an ICU Airway Plan should also be subject to a review date
- in EPIC an ICU Airway Plan does not expire during the admission
- we will take a pragmatic stance and propose the following:
1. MISSING - There is no ICU Airway Plan completed - either one has never been documented OR incomplete documentation does not satisfy option A or option B above. (e.g. there is no data entered for Option A or B above). 
3. COMPLETED - An ICU Airway plan has been completed - satisfying option A or option B above and generating a _dt stamp
4. FOR REVIEW - An ICU Airway plan has been completed - satisfying option A or option B above and generating a _dt stamp, but it is now >14 days between the current time and the _dt stamp; but exclude those with a COMPLETED Airway Plan who have a 'Natural Airway' (from the Airway tab [Airway Flowsheet ID 24499] of the ICU Airway Plan) AND have a DAS Generic Airway Plan [Row ID 24498] = YES (same a Option A that have 'Natural Airway') - these do not need review 
5. An ICU Airway Plan can be superceded at any time if an entry is updated or new entry is made, this will generate a new _dt stamp

*note I have removed 'update required' as a label.*

## Summary Data 

Feeds into (i) front tile (live data) (ii) 'airway plan completed' SPC chart

**[A] Proportion of patients with 'Airway Plan Completed' - Front tile**
- represented as a fraction (cf all targets set)
- classify T03 as one ICU (do not split into T03 North & T03 South) 
- for each of the four ICUs, identify the number of current inpatients, this is the denominator
- DENOMINATOR = total number of current number of inpatients (on each respective ICU)
- NUMERATOR = current number of patients designated as COMPLETED and FOR REVIEW, and add them together <br> [you may want to simplify this to = TOTAL CURRENT INPATIENTS - MISSING, but we will need the other data later]

**[B] Number of patients with 'Airway Plan For Review' - Front tile**
- represented as a number: "Airway plan - for review: integer
- classify T03 as one ICU (do not split into T03 North & T03 South) 
- for each of the four ICUs, identify the number of current inpatients with a COMPLETED ICU Airway Plan that has a _dt >14 days from the current time, display the number
- exclude those with a COMPLETED Airway Plan who have a 'Natural Airway' (from the Airway tab [Airway Flowsheet ID 24499] of the ICU Airway Plan) AND have a DAS Generic Airway Plan [Row ID 24498] = YES (same a Option A that have 'Natural Airway') - these do not need review


**[D] Number of patients with 'Airway Plan Missing'**
- not represented on the front tile, but feeds into the floorplan 1 
- for each of the four ICUs, identify the number of current inpatients with a MISSING ICU Airway Plan 

## Classification (corresponds to floorplan labelling)


**[E] Floorplan 1: Airway Plan Completed** (corresponds to floorplan A Airway Plan)
- the floorplan displays live data (current state) on a bed by bed basis and is updated as new data is available
1. If 'Airway Plan Completed'; classify as 'airway plan complete'. 
2. If 'Airway Plan Missing' (not completed / partially completed), classify as 'airway plan missing'
3. If 'Airway Plan For Review'; design = classify as 'airway plan for review'
5. If bed is empty; classify as 'empty'


**[F] Airway Type** (corresponds to floorplan B Airway type and Turning)

*Note that for Floorplan B, patients can have multiple labels- see lines 145-151 below*


- for each of the four ICUs, for each patient, identify which option has been documented in the Airway tab [Airway Flowsheet ID 24499] of the ICU Airway Plan, retain _dt stamp and process the following:
- Natural Airway - discard
- Endotracheal Tube - designate as entotracheal
- Percutaneous Tracheostomy - designate as tracheostomy
- Surgical Tracheostomy - designate as tracheostomy
- Laryngectomy - designate as laryngectomy
- Other (free text) - discard
- for each of the four ICUs, for each patient, identify whether 'Endotracheal tube' or 'Tracheostomy' have been returned from the O2 delivery device [Flowsheet ID 3040109305], retain _dt stamp and process the following:
- Endotracheal tube - designate as entotracheal
- Tracheostomy - designate as tracheostomy
- All other data - discard
- determine whether any of the current inpatients have any of the following three airway types
  1. entotracheal (from Airway Flowsheet ID 24499 and O2 delivery device ID 3040109305), use data with most recent _dt stamp, if data with the same _dt then use data from O2 delivery device (3040109305)
  2. tracheostomy (from Airway Flowsheet ID 24499 and O2 delivery device ID 3040109305), use data with most recent _dt stamp, if data with the same _dt then use data from O2 delivery device (3040109305)
  3. laryngectomy (from Airway Flowsheet ID 24499), use data with most recent _dt stamp
     
**[F] DART Call** (corresponds to floorplan B Airway type and Turning Plan)


- for each of the four ICUs, for each patient, identify whether the DART option has been documented in the Emergency Teams tab [ICU AIRWAY PLAN TRACHE CALL 24504] of the ICU Airway Plan, retain _dt stamp, process the following:
- DART = YES 
- DART = NO

**[G] Airway Turning Plan** (corresponds to floorplan B Airway type and Turning Plan)

- for each of the four ICUs, for each patient, identify whether the Doctor Required option has been documented in the Turning Plan tab [TURNING PLAN DOC REQ 24508] of the ICU Turning Plan, retain _dt stamp, process the following:
- Doctor Required = YES 
- Doctor Required = NO
- for each of the four ICUs, for each patient, identify whether the Senior Nurse Required option has been documented in the Turning Plan tab [TURNING PLAN NURSE REQ 24509] of the ICU Turning Plan, retain _dt stamp, process the following:
- Senior Nurse Required = YES 
- Senior Nurse Required = NO
- if both [TURNING PLAN NURSE REQ 24509] and [TURNING PLAN NURSE REQ 24509] = YES  label patient as Doctor Required.
- if either [TURNING PLAN NURSE REQ 24509] and [TURNING PLAN NURSE REQ 2450] = YES and DART = YES, label patient as the turn required AND DART call. 

Note that for floorplan B, Airway Type and Turning, a patient can be labelled as a type of airway and type of turn and DARRT or any combination. Some examples:

a) a patient can be labelled as Doctor Led Turn or Nurse Led Turn= YES, DARRT = YES, and any type of airway designated (Endotracheal, Tracheostomy, Laryngectomy, or no artificial airway)

b) a patient can be labelled as Doctor Led Turn or Nurse Led Turn= YES, DARRT = NO, and any type of airway designated (Endotracheal, Tracheostomy, Laryngectomy, or no artificial airway)

c) a patient can be labelled as Doctor Led Turn or Nurse Led Turn= NO, DARRT =YES and any type of airway designated (Endotracheal, Tracheostomy, Laryngectomy, or no artificial airway)

**See content for all floorplans and legends for the design key that relates to multiple labels for this floorplan**


____
## SPC CHART

TBC weekly percentage of patients who have an airway plan. 



1. This is a weekly percentage (p-chart) SPC
2. Week defined as Monday 00:00 – Sunday 23:59
3. Calculate the number of patients who have been present on the unit in the week
4. Calculate the number of patients who have been present on the unit in the week who have had at least one (option A or B above) airway plan documented at any point in their admission. In other words... a patient admitted during a particular week who has an ICU stay that spans over more than that week may have had an airway plan documented on any previous week during their ICU admission. These patients should be included in the numerator.
   *note this means if a patient is admitted towards the end of the week and the airway plan is not completed until the following week, this would not factor into the numerator of the week of admission, but would in the following week in which the airway plan was completed.* 
6. Numerator = patients present in the current week who have had at least one airway plan during ICU admission
7. Denominator = Patients present in the current week

---
## APPENDIX - unused flow sheets, discard after code review

## EPIC Flowsheets <br>
**Components of the ICU Airway Plan**
ICU Airway Plan - Group ID G UCLH ICU AIRWAY PLAN [23864]

| Flowsheet | Row ID | Manual / Automatic / Calculated Input | Comments | Expected documentation frequency |
|-|-|-|-|-|
|Intubation grade | R UCLH ICU INTUBATION GRADE 37950 | Manual | Options: <br> - Grade 1 <br> - Grade 2a <br> - Grade 2b <br> - Grade 3 <br> - Grade 4 <br> - Other (free text)| On completion of airway plan |
| Plan B | R UCLH ICU AIRWAY PLAN B 23866 | Manual | Free text | On completion of airway plan (if DAS Generic Airway Plan = No and PLAN A completed) |
| Plan C | R UCLH ICU AIRWAY PLAN A 23867 | Manual | Free text | On completion of airway plan (if DAS Generic Airway Plan = No and PLAN B completed) |







