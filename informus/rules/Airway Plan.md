# Airway Plan Rules
Rules for the Airway Plan Metric

## EPIC
Airway plan is completed in 'ICU Navigators' tab [doctors' log in view] and are displayed in 'Airway and Turning Plan' Tab.

The medical team should complete the airway plan at least once during the patient's admission to critical care.  If there are changes to the patient's airway status, then the airway plan should be updated.

ICU Airway Plan is a binary metric (an airway plan is either completed or not completed).

Inforum_us will display if the airway plan has been documented once during the patients admission.

## EPIC Flowsheets

 | Flowsheet | Row ID | Manual/Automatic/Calculated Input | Comments | Expected documentation frequency|
 |-|-|-|-|-|
| ICU Airway Plan | 23864 | Manual| | At least once an admission|
| Airway plan A | 23865 | Manual ||Once an admission (if DAS airway plan parameter is no)|
| Airway plan B| 23866|Manual| | |
| Airway plan C | 23867|Manual | | |
|O2 delivery|3040109305|Manual| Drop down (free text available)| Hourly (varies depending on patient's clinical condition)|


## Eligibility
All patients across all units *(what about patients that are end of life?)*

## Validity (time window) Rules: 

All patients should have an airway plan documented during admission to critical care. Airway plan documentation is considered valid until the patient is discharged from critical care.  However, there is an expectation that the airway plan will be updated if changes occur in the management of a patient's airway. For example: if patient has an artificial airway inserted or removed. *(Is this true if the type of airway is altered during the patient's stay? Is it possible to capture this?')* 

An airway plan is considered complete if any of the following is true:
 - DAS airway plan reads 'YES' *(don't think we have flowsheet for this - ID: 24498)*
 - DAS airway plan reads 'NO' but rows Airway plan A, Airway plan B and/or Airway plan C are completed. 
 - Either rows Airway plan A, Airway plan B and/or Airway plan C are filled in.
   *(Does rows airway plan A, airway plan B and airway plan C all need to be filled in to be valid if not following generic airway plan?)*
   
An airway plan can be superseded if an entry is updated or new entry is made, this will generate a new _dt stamp (more recent) and become the 'valid' entry

## Classification

**[A] Proportion of patients with 'Airway Plan Completed'**

Feeds into (i) front tile (current time snapshot), (ii) (?) floorplan and (iii) 'airway plan completed' SPC chart

**FRONT TILE proportion of patients with 'airway plan completed'**

The front tile displays live data (i.e. the current state on each unit)
For each patient, an airway plan is considered (1) COMPLETED if any of the following is true;

 - DAS airway plan reads 'YES'*(don't think we have flowsheet for this - ID: 24498)*
 - DAS airway plan reads 'NO' but rows Airway plan A, Airway plan B and/or Airway plan C are filled in.
 - Either rows Airway plan A, Airway plan B and/or Airway plan C are filled in.
   *(Does rows airway plan A, airway plan B and airway plan C all need to be filled in to be valid if not following generic airway plan?)*

If none of the following flowsheets are completed: DAS airway (with a reading of YES) or Airway Plan A, B or C then Airway Plan is (2) NOT COMPLETED.

Numerator = sum of patients achieving (1) COMPLETED response

Denominator = total number of current patients (occupied beds)

Calculation: (numerator / denominator)*100 represented as percentage *(we want to express as a percentage as all targets is not?)*

**[B] Floorplan labelling** *(This is assuming that the dashboard is only displaying airway plan completed and not looking at other parameters such as difficult or altered airway)*

The floorplan displays live data (current state) on a bed by bed basis and is updated as new data is available (outcome is binary and there is no option for 'missing data')

If 'airway plan completed'; design = green filled bed

If 'airway plan not completed'; design = red filled bed

If bed is empty; design = white filled bed with dark grey outline

---
## SPC CHART








