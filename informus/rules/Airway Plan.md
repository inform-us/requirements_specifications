# Airway Plan 
Rules for the Airway Plan [completed] Metric


## EPIC
- the ICU Airway Plan is completed by doctors
- it is accessed in ICU Navigators - Airway and Turning [doctors' log in view]
- in addition, if an 'Airway Alert' exists (left hand side of EPIC screen with allergies and other alerts), clicking on it will also take you to the ICU Airway Plan
- the medical team should complete the ICU Airway Plan on admission to critical care, following assessment of any new upper airway pathology and after any procedure involving the airway (e.g. re-intubation, tracheostomy, bronchoscopy, difficult nasogastric tube insertion, SL&T review etc)
- some of above review triggers are either more nuanced (subtle clinical changes) or rely on free text entry in EPIC - these will not be considered
- other review triggers are more certain and are documented in EPIC flowsheets (e.g new endotracheal tube insertion or tracheostomy insertion)
- there is currently no concensus on whether an ICU Airway Plan should also be subject to a review date (cf ICU targets), separate to the triggers mentioned above
- the most favoured opinion is a 7 day validity [further information to follow]
- ICU Airway Plan is a binary metric (an airway plan is either completed or not completed)


## EPIC Flowsheets
**Components of the ICU Airway Plan**
ICU Airway Plan - Group ID G UCLH ICU AIRWAY PLAN [23864]

| Flowsheet | Row ID | Manual / Automatic / Calculated Input | Comments | Expected documentation frequency |
|-|-|-|-|-|
| Airway | R UCLH ICU AIRWAY PLAN 24499 | Manual | Options: <br> - Natural Airway <br> - Endotracheal Tube <br> - Percutaneous Tracheostomy <br> - Surgical Tracheostomy <br> - Laryngectomy <br> - Other (free text) | On completion of airway plan |
|Intubation grade | R UCLH ICU INTUBATION GRADE 37950 | Manual | Options: <br> - Grade 1 <br> - Grade 2a <br> - Grade 2b <br> - Grade 3 <br> - Grade 4 <br> - Other (free text)| On completion of airway plan |
| DAS Generic Airway Plan | R UCLH ICU AIRWAY PLAN DAS 24498 | Manual | Options: <br> - Yes <br> - No <br> - Other (free text) | On completion of airway plan |
| Plan A | R UCLH ICU AIRWAY PLAN A 23865 | Manual | Free text | On completion of airway plan (if DAS Generic Airway Plan = No) |
| Plan B | R UCLH ICU AIRWAY PLAN B 23866 | Manual | Free text | On completion of airway plan (if DAS Generic Airway Plan = No and PLAN A completed) |
| Plan C | R UCLH ICU AIRWAY PLAN A 23867 | Manual | Free text | On completion of airway plan (if DAS Generic Airway Plan = No and PLAN B completed) |
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
| O2 delivery device |R OXYGEN DELIVERY METHOD 3040109305 | Drop down (free text available) |Select drop down options: <br> Nasal cannula <br> Simple mask <br> Venturi mask <br> Capno mask <br> High-flow nasal cannula (HFNC) <br> Humidified oxygen mask <br> Non-rebreather mask <br> Tracheostomy mask <br> CPAP/Bi-PAP mask <br> Oxyhood <br> Bag valve mask (BVM) <br> Endotracheal tube <br> Tracheostomy <br> Other (comment) <br> No respiratory support provided | Hourly (varies depending on patient's clinical condition)|

ETT Properties Row ID 3040102626 links to LDA AVATAR Placement Date Row ID 700 Placement Time Row ID 701 <br>
Surgical Airway Properties Row ID 700004 links to LDA AVATAR Placement Date Row ID 700 Placement Time Row ID 701

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
 - DAS airway plan reads 'NO' but Airway plan A has been completed within the last seven days.
 - Either Airway plan A, Airway plan B and/or Airway plan C are filled in within the **last seven days**.
   

If none of the following flowsheets are completed within the last seven days: DAS airway (with a reading of YES) or Airway Plan A, B or C then Airway Plan is (2) NOT COMPLETED.

Numerator = sum of patients achieving (1) COMPLETED response

Denominator = total number of current patients (occupied beds)

Calculation: (numerator / denominator)


*(NOTE: For second version of metric)*
If a patient has a new airway inserted or removed, the Airway Plan will switch to (2) NOT COMPLETED until any of the documentation specified for COMPLETED is redone. 


**Floorplan labelling: Patients in Critical Care: Airway Plan Completed** 

The floorplan displays live data (current state) on a bed by bed basis and is updated as new data is available (outcome is binary and there is no option for 'missing data')

If 'airway plan completed'; design = green filled bed

If 'airway plan not completed'; design = red filled bed

If 'airway plan completed but >7 days old'; design - orange filled bed

If bed is empty; design = white filled bed with dark grey outline

Secondary "airway managment" labelling

If a patient is labelled as doctor led turn; an icon "Dr" will be present on bed 
If a patient is labelled as senior nurse led turn; an icon "SN" will be present on bed.  *(However, if a patient is also labelled as doctor led turn, the label will be doctor led turn as primary label i.e. a reading of doctor led turn overides the label of senior led turn)*
If a patient has neither doctor led turn or senior led turn label *or DART label*, the bed space will not have an secondary label.

*(NOTE: For second version of metric - when flowsheet for "emergency teams" become available on EMAP)*
If a patient is labelled as DART: an icon spelling DART will be present on bed.

---

**[C] Future floorplan labelling: Airway Present**



## SPC CHART








