
# Perioperative Medicine (POM) DrEaMing (Drinking, Eating and Mobilising) Metrics 
Rules for POM DrEaMing metrics


## EPIC
The POM DrEaMing Metrics refer to the status of post-operative patients' Drinking Eating and Mobilising.

These data are input manually by nurses at least once every 24 hours or every time a patient Drinks, Eats or Mobilises

The metrics are labeled as fluid intake, diet intake and moblisation acheieved in EPIC

Inform_us will display whether the nurse has documented the status of drinking, eating and mobilising in the last 24 hours and each patient's status on the three components


## EPIC Flowsheets

The flowsheets exist in Post-Op Surgical tab of ICU navigators

FLUID INTAKE [45429]

DIET INTAKE [6482]

MOBILISATION ACHIEVED [40705] levels of mobilisation are from 0-10 from lying in bed to walking independently

MOBILITY SCALE [1102] is the scale that the physios use 


## ELIGIBILITY
All patients on T06 or WMS units

## VALIDITY
Fluid intake, diet intake and mobilisation achieved metrics are valid for 24 hours from 00:01 hours each day or until a new entry has been made 


For eligible patients, fluid intake, diet intake and mobilisation achieved metrics should be documented once every 24 hours or until a patient's status changes. 


## CLASSIFICATION
The following data feeds into (i) the dial on the front tile (ii) POM DrEaMing documentation SPC chart

POM DrEaMing Percentage Completions today (since midnight)

Includes all patients present on T06 and WMS since 00:00 today

Numerator = number of patients who have DrEaMing (all three of fluid intake, diet intake and mobilisation achieved) documented (anything other than missing) at least once since 00:00 today until now

Denominator = number of patients who have been present since 00:00 today until now

*note compliance with the documentation is binary and patient must have all three documented to be considered compliant with documentation*


 
## Labelling Rules: (corresponds to the floor plans)

There will be 3 separate floorplans with Fluid intake to be default and buttons to select the others (see e.g. MAP and SPO2 SPC charts)
FLUID INTAKE FLOORPLAN

1. if the latest 'fluid intake' reading is 'IV ongoing' then label patient as 'IV ongoing'
2.  if the latest 'fluid intake' reading is 'IV discontinued' then label patient as 'IV discontinued'
3.  if the latest 'fluid intake' reading is 'oral fluids' then label patient as 'oral fluids' TBC
4.  if the latest 'fluid intake' reading is 'NBM' then label patient as 'NBM'
5.  if 'fluid intake' has not been completed since 00:00 today, then label patient as 'missing'
6.  if none of the rules matched then label the patient as 'fallthrough'
   
  *n.b. fallthrough is shown as dark grey bed on floorplan, but there is no accompanying legend item. This is explained to user in ? button.*

DIET INTAKE FLOORPLAN

1. if the latest 'diet intake' reading is 'normal diet' or 'soft diet' then label patient as 'eating and drinking'
2.  if the latest 'diet intake' reading is 'free fluids' or 'clear fluids' then label patient as 'fluid only'
3.  if the latest 'diet intake' reading is 'enteral (NG/PEG etc.)' or 'parenteral (TPN)' then label patient as 'enteral/parenteral feeding'
5.  if the latest 'diet intake' reading is 'NBM' then label patient as 'NBM'
6.   if the latest 'diet intake' reading is 'sips' then label patient as 'sips only'
7.  if the latest 'diet intake' reading is 'other' then label patient as 'other'
8.  if 'diet intake' has not been completed since 00:00 today, then label patient as 'missing'
9.  if none of the rules matched then label the patient as 'fallthrough'
   
  *n.b. fallthrough is shown as dark grey bed on floorplan, but there is no accompanying legend item. This is explained to user in ? button.*   
  
MOBILISATION ACHIEVED FLOORPLAN - **DRAFT FOR NOW as We've come up against some issues with staff here. Hold off on this build.** 

1. if the latest 'mobilisation achieved' reading is 'nothing (lying in bed) 0' or 'sitting in bed, exercises in bed 1' or 'passively moved to chair (no standing) 2'or 'sitting over edge of the bed 3' then label patient as 'in bed' 
2. if the latest 'mobilisation achieved' reading is 'standing 4' then label patient as 'standing'
3.  if the latest 'mobilisation achieved' reading is 'transferring bed to chair 5' then label patient as 'chair' 
4.  if the latest 'mobilisation achieved' reading is 'marching on spot (at bedside) 6' then label patient as 'marching on spot'
5.  if the latest 'mobilisation achieved' reading is 'walking with assistance of 2 or more people 7' or 'walking with assistance of 1 person 8' label patient as 'walking with assistance'
6.   if the latest 'mobilisation achieved' reading is 'walking independently with gait aid 9 ' or 'walking independently without gait aid 10' label patient as 'walking independently'
7. If 'mobilisation achieved' has not been completed since 00:00 today, then label patient as 'missing'
8. If none of the rules matched then label the patient as 'fallthrough'

   *n.b. fallthrough is shown as dark grey bed on floorplan, but there is no accompanying legend item. This to be explained to user in ? button.*


## SPC Chart: (corresponds to the DrEaMing documentation SPC chart)

 Daily POM DrEaMing Documentation 

Proportion of 'POM DrEaMing' documented in EPIC

Operational definition = of all Perioperative patients (patients on T06 and WMS), what proportion have daily DrEaMing metrics (fluid intake, diet intake, mobilisation achieved) documented (weekly chart) 

A day is defined as between 00:00 and 23:59 
A week is defined as 00:00 on Monday to 23:59 on the following Sunday

To comply with the DReaMing metric, all three (fluid intake, diet intake, mobilisation achieved) must be documented at least once in this time window (i.e. a valid _dt stamp for an entry for each individual metric) in order for each patient to achieve (1) Documented for that patient

If any of the 3 DReaMing metrics are missing for any patient, an entry (a valid _dt stamp) then do not count 

Numerator = sum of patients achieving (1) Documented response between 00:00 and 23:59 
Denominator = total number of patients (occupied beds) between 00:00 and 23:59 

Calculate daily percentage for each unit

Aggregate the daily percentages into a -weekly mean percentage_ for each of these respective units (T06, WMS)
?calculate weekly percentage without aggregation? 

Plot an SPC chart for each respective unit: y-axis = weekly percentage; x-axis = time

