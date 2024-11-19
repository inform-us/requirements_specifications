# Airway Plan 
Rules for the completed Airway Plan Metric

## EPIC
Airway plan is completed in 'ICU Navigators' tab [doctors' log in view] and are displayed in 'Airway and Turning Plan' Tab, as well as being accessed through the 'Airway ALert' tab on the left hadn side bar in EPIC

The medical team should complete the airway plan on admission, after airway instrumnetation or change of status (e.g intubation, bronchoscopy , percutaneous tracheostomy, SL&T review etc) as well a a weekly review therafter. 
If there are changes to the patient's airway status, then the airway plan should be updated.

ICU Airway Plan is a binary metric (an airway plan is either completed or not completed).

Inforum_us will display if the airway plan has been documented during the patients admission.

## EPIC Flowsheets

| Flowsheet | Row ID | Manual/Automatic/Calculated Input | Comments | Expected documentation frequency|
|-|-|-|-|-|
|Airway| 24499| Manual| Options available (free text available)|On completion of airway plan |
| DAS generic Airway Plan | 24498 | Manual|Options available (free text available) | Weekly|
| Airway plan A | 23865 | Manual |Free text|Weekly (if DAS airway plan parameter is no)|
| Airway plan B| 23866|Manual|Free text | |
| Airway plan C | 23867|Manual |Free text| |
|Intubation grade| 37950| Manual |Options available (free text available) | On completion of airway plan |
|O2 delivery|3040109305|Manual| Drop down (free text available)| Hourly (varies depending on patient's clinical condition)|


## Eligibility
All patients across all units 

## Validity (time window) Rules: 

All patients should have an airway plan documented during admission to critical care. Airway plan documentation is considered valid for one week unless a new artifical airway is inserted or removed (i.e. a tracheostomy or endotracheal tube). *(Note that this is not official guidelines currently)* 
An airway plan can be superseded if an entry is updated or new entry is made, this will generate a new _dt stamp (more recent) and become the 'valid' entry

If an new artifical airway is inserted or removed *(Does removal of an airway warrent a new airway plan?)* than the previous airway plan is considered invalid and a new airway plan should been completed. 
*(Currently awaiting flowsheets to enable identification of insertion/removal of new airways so this will be included in the second version of metric)*


## Classification

**[A] Proportion of patients with 'Airway Plan Completed'**

Feeds into (i) front tile (current time snapshot), (ii) floorplan and (iii) 'airway plan completed' SPC chart

**FRONT TILE proportion of patients with 'airway plan completed'**

The front tile displays live data (i.e. the current state on each unit)
For each patient, an airway plan is considered (1) COMPLETED if any of the following is true;

 - DAS airway plan reads 'YES' and has been completed within the last seven days.
 - DAS airway plan reads 'NO' but rows Airway plan A (Airway plan B and/or Airway plan C are completed within the last seven days).
 - Either rows Airway plan A, Airway plan B and/or Airway plan C are filled in within the **last seven days**.
   *(Does rows airway plan A, airway plan B and airway plan C all need to be filled in to be valid if not following generic airway plan?)*

If none of the following flowsheets are completed within the last seven days: DAS airway (with a reading of YES) or Airway Plan A, B or C then Airway Plan is (2) NOT COMPLETED.

Numerator = sum of patients achieving (1) COMPLETED response

Denominator = total number of current patients (occupied beds)

Calculation: (numerator / denominator)*100 represented as percentage *(Do we want to express as a percentage?)*


*(NOTE: For second version of metric)*
If a patient has a new airway inserted or removed, the Airway Plan will switch to (2) NOT COMPLETED until any of the documentation specified for COMPLETED is redone. 


**Floorplan labelling: Patients in Critical Care: Airway Plan Completed** 

The floorplan displays live data (current state) on a bed by bed basis and is updated as new data is available (outcome is binary and there is no option for 'missing data')

If 'airway plan completed'; design = green filled bed

If 'airway plan not completed'; design = red filled bed

If 'airway plan completed but >7 days old'; design - orange filled bed

If bed is empty; design = white filled bed with dark grey outline

*(Would having an amber category for patients that have had an airway plan completed this admission but not currently valid or is this complicationg things?)*

---

**[C] Future floorplan labelling: Patients in Critical Care: Airway Management** 

This is a seperate floorplan with Airway Plan Completed to be default and a button to select Airway Management.  
*(Note: Awaiting activation of flowsheets in EMAP therefore this floorplan is for future development)*

The floorplan displays live data (current state) on a bed by bed basis and is updated as new data is available.   

If a patient is labelled as doctor led turn; design = red filled bed. 
If a patient is labelled as senior nurse led turn; design = amber filled bed.  However, if a patient is also labelled as doctor led turn, the label will be doctor led turn as primary label i.e. a reading of doctor led turn overides the label of senior led turn.
If a patient has neither doctor led turn or senior led turn label: design = white filled bed.

Secondary 'emergency teams' labeling

In addition to the above labeling, if the latest 'emergency team@ reading is 'DART' then also label patient as 'DART'. Note this means that some patients who have 'DART' may have two labels, a primary label as per steps above and a potential secondary label.  We need to denote this somehow on the floorplan as well. Bed is filled with the primary label as well as the letters DART.

*(Do we need to know the other emergency teams?)*

## SPC CHART








