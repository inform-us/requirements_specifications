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
| ICU (DAS) Airway Plan | 23864 | Manual| | At least once admission|
| Airway plan A | 23865 | Manual |||
| Airway plan B| 23866|Manual| | |
| Airway plan C | 23867|Manual | | |
|O2 delivery|3040109305|Manual| Drop down (free text available)| Hourly (varies depending on patient's clinical condition)|


## Eligibility
All patients across all units *(what about patients that are end of life?)*

## Validity (time window) Rules: 

All patients should have an airway plan documented during admission. Documentation of an airway plan is considered valid for the duration of the patient's stay on critical care. I.e. from documentation of airway plan until discharge of the patient *(Is this true if the type of airway is altered during the patient's stay? Is it possible to capture this?')* 

An airway plan is considered complete if the following is true:
 - DAS airway plan reads 'YES'
 - DAS airway plan reads 'NO' but rows Airway plan A, Airway plan B and/or Airway plan C are filled in.
 - Either rows Airway plan A, Airway plan B and/or Airway plan C are filled in.
   *(Does rows airway plan A, airway plan B and airway plan C all need to be filled in to be valid if not following generic airway plan?)*
   
An airway plan can be superseded if an entry is updated or new entry is made, this will generate a new _dt stamp (more recent) and become the 'valid' entry

## Classification



