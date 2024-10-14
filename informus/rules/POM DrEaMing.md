
# Perioperative Medicine (POM) DrEaMing (Drinking, Eating and Mobilising) Metrics 
Rules for DrEaMing metrics


## EPIC
The DrEaMing Metrics refer to the status of post-operative patients' Drinking Eating and Mobilising.

These data are input manually by nurses at least once every 24 hours and ideally every time a patient Drinks, Eats or Mobilises

The metrics are labeled as fluid intake, diet intake and moblisation achieved in EPIC

Inform_us will display whether staff have documented the status of drinking, eating and mobilising in the last 24 hours and each patient's status on the three components


## EPIC Flowsheets

 | Flowsheet | Row ID | Manual/Automatic/Calculated Input | Comments |
  |-|-|-|-|
 | Fluid Intake | 45429 | Manual | Drop down (free text possible)|
 | Diet Intake | 6482 | Manual | Drop down (free text possible)|
 | Mobisation Achieved | 40705 | Manual | Drop down (free text possible)|
|Reasons for not mobilising | 47371 | Manual | Drop down| 

 
The flowsheets exist in Post-Op Surgical tab of ICU navigators

**FLUID INTAKE [45429] the nurse will document whether a patient's fluid intake is:**  

- intravenous 'IV Ongoing'

- previously intravenous 'IV Discontinued'

- drinking normally 'oral fluids' or

- nil by mouth/not allowed any oral fluid or food intake 'NBM'
  

**DIET INTAKE [6482] the nurse will document whether a patient's diet intake is:** 

-  oral: 'normal diet' or 'soft diet' or 'pureed' or 'nutritional supplement'

-   fed through a feeding tube 'enteral (NG/PEG etc.)'

-   fed directly into the vein 'parenteral (TPN)'

-   is having only sips of water 'sips'

-   is on a fluid restriction diet 'fluid restriction' or 
  
-   nil by mouth/not allowed any oral fluid or food intake 'NBM'. There is also an 'other' option for diet intake. 

**MOBILISATION ACHIEVED [40705] levels of mobilisation are documented by physiotherapist or nurse when staff are attempting to mobilise.**

The scale ranges from 0-10 and in T06 and WMS we aim to get post-operative patients to level 5 within a few hours of surgery and walking on day one unless their baseline mobility will not allow for this. 

0 - patient is lying in bed

1- patient is sitting in bed or doing exercises in bed 

2- patient is being passively moved to chair, but cannot stand

3- patient can sit over edge of the bed

4- patient can stand

5- patient can transfer from bed to a chair 

6- patient can march on spot at bedside 

7- patient can walk with the assistance of 2 or more people

8- patient can walk with assistance of 1 person 

9- patient can walk independently with gait aid 

10- patient can walking independently without gait aid 

## ELIGIBILITY
All patients on T06 or WMS units

## VALIDITY
Fluid intake, diet intake and mobilisation achieved metrics are valid for 24 hours from 00:00 hours each day or until a new entry has been made 


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
3.  if the latest 'fluid intake' reading is 'oral fluids' then label patient as 'oral fluids' 
4.  if the latest 'fluid intake' reading is 'NBM' then label patient as 'NBM'
5.  if 'fluid intake' has not been completed since 00:00 today, then label patient as 'missing'
6.  if none of the rules matched then label the patient as 'fallthrough'
   
  *n.b. fallthrough is shown as dark grey bed on floorplan, but there is no accompanying legend item. This is explained to user in ? button.*

DIET INTAKE FLOORPLAN

1. if the latest 'diet intake' reading is 'normal diet' or 'soft diet' or 'pureed' or 'nutritional supplement' then label patient as 'eating and drinking'
2. if the latest 'diet intake' reading is 'free fluids' or 'clear fluids' then label patient as 'fluid only'
3. if the latest 'diet intake' reading is 'enteral (NG/PEG etc.)' or 'parenteral (TPN)' then label patient as 'enteral/parenteral feeding'
5. if the latest 'diet intake' reading is 'NBM' then label patient as 'NBM'
6. if the latest 'diet intake' reading is 'sips' then label patient as 'sips only'
7. if the latest 'diet intake' reading is 'other' then label patient as 'other'
8. if the latest 'diet intake' reading is 'fluid restriction' then label the patient as 'fluid restriction' 
9.  if 'diet intake' has not been completed since 00:00 today, then label patient as 'missing'
10.  if none of the rules matched then label the patient as 'fallthrough'
   
  *n.b. fallthrough is shown as dark grey bed on floorplan, but there is no accompanying legend item. This is explained to user in ? button.*   

MOBILISATION ACHIEVED FLOORPLAN 

1. if the latest 'mobilisation achieved' reading is 0, 1, 2 or 3 then label patient as 'in bed' 
2. if the latest 'mobilisation achieved' reading is 4, 5 or 6 then label patient as 'actively transferring'
5.  if the latest 'mobilisation achieved' reading is 7 or 8, then label patient as 'walking with assistance'
6.   if the latest 'mobilisation achieved' reading is 9  or 10, then  label patient as 'walking independently'
7. If 'mobilisation achieved' has not been completed since 00:00 today, then label patient as 'missing'
8. If none of the rules matched then label the patient as 'fallthrough'

   *n.b. fallthrough is shown as dark grey bed on floorplan, but there is no accompanying legend item. This to be explained to user in ? button.*
  ## Alternative version Labelling Rules: (corresponds to the floor plans)

There will be 3 separate floorplans with Eating and Drinking  to be default and buttons to select the others (see e.g. MAP and SPO2 SPC charts)

EATING AND DRINKING FLOORPLAN

1. if the latest 'diet intake' reading is 'normal diet' or 'soft diet' or 'pureed' or 'nutritional supplement' then label patient as 'eating and drinking'. Bed to be green filled. 
2.  if the latest 'diet intake' reading is 'sips' then label patient as 'sips of water'. Bed to be orange filled. 
3.  if the latest 'diet intake' reading is 'free fluids',  or if the latest 'fluid intake' reading is 'oral fluids', then label patient as 'free fluids'. Bed to be blue filled. 
4. if the latest 'diet intake' reading is 'clear fluids' then label patient as 'clear fluids'. Bed to be yellow filled.
5. if the latest 'diet intake' reading is 'enteral (NG/PEG etc.)' or 'parenteral (TPN)' then label patient as 'enteral/parenteral feeding'. Bed to be violet filled. 
6. if the latest 'fluid intake' or 'diet intake' reading is 'NBM' then label patient as 'NBM'. Bed to be red filled. 
7.  if the latest 'diet intake' reading is 'other' then label patient as 'other'. Bed to be light grey filled.
9.  if both 'diet intake' AND 'fluid intake' flowsheets have not been completed since 00:00 today, then label patient as 'missing'. Bed to be red hashed outline and no fill.
   Secondary eating and drinking labelling 
10.  in addition to the above labelling, if the latest 'fluid intake' reading is 'IV ongoing' then also label patient as 'IV ongoing'. Note this means that some patients who have 'IV ongoing' will have two labels, a primary label as per steps 1-8 and and a potential secondary label for example if the patient is on an IV and also drinking fluids. We need to denote this somehow on the floorplan as well. Bed is filled with the primary label as above with an outline denoting IV- blue outline? 
11.   if none of the rules matched then label the patient as 'fallthrough' 
   
  *n.b. fallthrough is shown as dark grey bed on floorplan, but there is no accompanying legend item. This is explained to user in ? button.*

MOBILISATION ACHIEVED FLOORPLAN 

1. if the latest 'mobilisation achieved' reading is 0, 1, 2 or 3 then label patient as 'in bed' 
2. if the latest 'mobilisation achieved' reading is 4, 5 or 6 then label patient as 'actively transferring'
5.  if the latest 'mobilisation achieved' reading is 7 or 8, then label patient as 'walking with assistance'
6.   if the latest 'mobilisation achieved' reading is 9  or 10, then  label patient as 'walking independently'
7. If 'mobilisation achieved' has not been completed since 00:00 today, then label patient as 'missing'
8. If none of the rules matched then label the patient as 'fallthrough'

DOCUMENTATION COMPLIANCE FLOORPLAN

1. if all three DrEaMing flowsheets- 'fluid intake', 'diet intake' and 'moblisation acheived' flowsheets have not been completed since 00:00 today, then label patient as 'Missing DReaMING Documentation'. Bed to be red hash outline. 
2. if one or two of the 'fluid intake', 'diet intake' or 'moblisation acheived' flowsheets have been completed since 00:00 today,  then label patient as 'DrEaMing Partially Documented'. Bed to be amber filled. 
3. if all three DrEaMing flowsheets- 'fluid intake', 'diet intake' and 'moblisation acheived' flowsheets have been completed since 00:00 today, then label patient as 'DReaMING Documentation Complete'. Bed to be green filled. 
   
## SPC Chart: (corresponds to the DrEaMing documentation SPC chart)

 Daily POM DrEaMing Documentation 

Proportion of 'POM DrEaMing' documented in EPIC

Operational definition = of all Perioperative patients (patients on T06 and WMS), what proportion have daily DrEaMing metrics (fluid intake, diet intake, mobilisation achieved) documented (weekly chart) 

A day is defined as between 00:00 and 23:59 
A week is defined as 00:00 on Monday to 23:59 on the following Sunday

To comply with the DReaMing metric, all three (fluid intake, diet intake, mobilisation achieved) must be documented at least once in this time window (i.e. a valid _dt stamp for an entry for each individual metric) in order for each patient to achieve (1) DReaMing documented 

If any of the 3 DReaMing metrics are missing for any patient, an entry (a valid _dt stamp) then do not count 

Numerator = sum of patients achieving (1) Documented response between 00:00 and 23:59 

Denominator = total number of patients present on unit (based on MRNs) between 00:00 and 23:59 

Calculate daily percentage for each unit

Aggregate the daily percentages into a -weekly mean percentage_ for each of these respective units (T06, WMS)
?calculate weekly percentage without aggregating? - this does not account for patients with admission over 1 day... 

Plot an SPC chart for each respective unit: y-axis = weekly percentage; x-axis = time

