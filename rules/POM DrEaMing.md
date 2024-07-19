
# Perioperative Medicine (POM) DrEaMing (Drinking, Eating and Mobilising) Metrics 
Rules for POM DrEaMing metrics


## EPIC
The POM DrEaMing Metrics refer to the status of post-operative patients' Drinking Eating and Mobilising.

These data are input manually by nurses at least once every 24 hours or every time a patient Drinks, Eats or Mobilises

The metrics are labeled as fluid intake, food intake and moblisation acheieved in EPIC

Inform_us will display whether the nurse has documented the status of drinking, eating and mobilising in the last 24 hours and each patient's status on the three components


## EPIC Flowsheets

The flowsheets exist in Post-Op Surgical tab of ICU navigators

FLUID INTAKE [45429]

FOOD INTAKE [6482]

MOBILISATION ACHIEVED [40705]


## ELIGIBILITY
All patients on T06 or WMS units

## VALIDITY
Fluid intake, food intake and mobilisation achieved metrics are valid for 24 hours from 00:01 hours each day or until a new entry has been made 


For eligible patients, fluid intake, food intake and mobilisation achieved metrics should be documented once every 24 hours or until a patient's status changes. 


## CLASSIFICATION
The following data feeds into (i) the text at the bottom POM DrEaMing front tile (ii) POM DrEaMing documentation SPC chart

POM DrEaMing Percentage Completions today (since midnight)

Includes all patients present on T06 and WMS since 00:01 today

Numerator = number of patients who have DrEaMing (all three of fluid intake, food intake and mobilisation achieved) documented at least once since 00:01 today

Denominator = number of patients who have been present since 00:01 today

*note compliance with the documentation is binary and patient must have all three documented to be considered compliant with documentation*


 
## Labelling Rules: (corresponds to the floor plans)

FLUID INTAKE FLOORPLAN
1. if the latest 'fluid intake' reading is 'IV ongoing' then label patient as 'IV ongoing'
2.  if the latest 'fluid intake' reading is 'IV discontinued' then label patient as 'IV discontinued'
3.  if the latest 'fluid intake' reading is 'oral fluids' then label patient as 'oral fluids' 
4.  if the latest 'fluid intake' reading is 'NBM' then label patient as 'NBM'
5.  if 'fluid intake' has not been completed since 00:01 today, then label patient as 'missing documentation 
if the latest 2 consecutive hours are both classified as 'below' then label patient as 'below'
if the latest classification is 'not applicable' then label the patient as 'not applicable'
if there are 5 non-consecutive hours in the 24hr timeseries classified as either 'below' or 'above', count backward and label the patient the majority label
if the latest hour is classified as 'in range', then label patient as 'in range'
if the latest classification is 'non-numerical' then label the patient as 'non-numerical'
if the latest classification is 'missing' then label the patient as 'missing'
if the latest classification is 'not set' then label the patient as 'not set'
if the classification was 'in range' and is now above(below) for fewer than 3(2) hours then label as 'in range'
if none of the rules matched then label the patient as 'fallthrough'
n.b. fallthrough is shown as dark grey bed on floorplan, but there is no accompanying legend item. This is explained to user in ? button.




Floor plan 
Are we looking at who 
Are we looking at who is DrEaMing? Bespoke. 
