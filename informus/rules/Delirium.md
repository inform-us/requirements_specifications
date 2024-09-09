# Delirium  
Rules for Delirium using CAM-ICU Metric (confusion assessment method-intensive care unit)

## EPIC
- Delirium metric is a binary score, nurses input this manually
- The score is required on all patients that have a (valid) RASS score (e.g. includes forward filled RASS scores) of -3 to +4 during any 12-hour shift
- The two possible outcomes for CAM-ICU score are positive or negative
- A positive score denotes that a patient has delirium, a negative score denotes that a patient does not have delirium
- There are no targets for these variables, however we endeavour clinically to have as few positive scores as we can

## EPIC Flowsheets
- CAM-ICU has 4 components (feature 1-4, see CAM-ICU EPIC_flowsheet PDF) to generate an 'overall' CAM-ICU; the components are not required for this metric

### Group ID CAM-ICU
- CONFUSION ASSESSMENT METHOD-ICU (CAM-ICU) [3040104646]

### Row ID CAM-ICU

- R CAM-ICU FEATURE 1: ACUTE ONSET OR FLUCTUATING COURSE [3040104645]
- R CAM-ICU FEATURE 2: INATTENTION [3040104647]
- R CAM-ICU FEATURE 3: ALTERED LEVEL OF CONSCIOUSNESS [3040104648]
- R CAM-ICU FEATURE 4: DISORGANIZED THINKING [3040104649]
- R CAM-ICU OVERALL [3040104650] (this is the flowsheet that we pull the data from for delirium metric. Is autopopulated from the above) 



[CAM-ICU EPIC_flowsheet.pdf](https://github.com/user-attachments/files/16235096/CAM-ICU.EPIC_flowsheet.pdf)

### Group ID Richmond Agitation Sedation Scale (RASS)
- G UCLH ICU NEW NEUROLOGY [39859]

### Row ID RASS
- R RICHMOND AGITATION SEDATION SCALE (RASS) [3040104644]

---
To be INSERT PDF -  ABC metric user interface sequence once built on staging (flowchart on how you navigate through the dashboard) 
---

## ELIGIBILITY 
- All patients who have a valid RASS score between -3 to +4 this shift

*note If a patient has a RASS score of <-3 documented, CAM-ICU cannot be generated on EPIC* check

### Clinical pragmatism
According to clinical guidelines:
	- a RASS score within the range above should trigger a CAM-ICU assessment
	- a CAM-ICU assessment should be done a minimum once a shift
	- best practice is to have a RASS & CAM-ICU charted concurrently
	- however, it is possible to be CAM-ICU positive (features 1, 2 & 4 positive) without a RASS being documented

Therefore we unlink the RASS from CAM-ICU, but highlight the absence of RASS documentation (if a CAM-ICU is charted without RASS). 

## VALIDITY

### RASS
- clinical guideline recommended charting frequency for RASS differs depending on time of day
- in line with other documentation we add 15 minutes leeway to the validity of the documented score to allow for clinical leeway

### RASS generate 
1) RASS scores documented between 06:00 - 21.59 is valid for 75 minutes
2) RASS scores documented between 22:00 - 05:59 is valid 255 minutes (4 hours & 15 minutes)

### CAM-ICU
1) For eligible patients (RASS -3 to +4), the CAM-ICU metric should be documented once per 12-hour shift 
2) 12-hour shifts are defined as:
- DAY SHIFT 08:00-19:59
- NIGHT SHIFT 20:00-07:59
3) Every CAM-ICU score set on a shift is valid until the end of the shift or until superseded by a subsequent documented score:
- DAY SHIFT (08:00-19:59) CAM-ICU score is valid until 19:59 hours or until a subsequent score is documented
- NIGHT SHIFT (20:00-07:59) CAM-ICU score is valid until 07:59 hours or until a subsequent score is documented
4) Each CAM-ICU score therefore expires at 07:59 or 19:59 every day. 
7) Each documented CAM-ICU score can be superseded if an entry is updated or new entry is made during that shift, this will generate a new _dt stamp (more recent) and become the 'valid' entry

## CLASSIFICATION 

*The following data feeds into (i) the text at the bottom of the Delirium front tile [and (ii) SPC CAM-ICU documentation chart]*

**[A] CAM-ICU Percentage Completion This Shift - Front Tile**
- This is a real time (cumulative) percentage that should head towards 100% by close of the current shift
- With each 'refresh' you are looking at the period from start of the shift to the current time
- Includes all patients present on the unit during the current shift (including discharged patients who were present during this shift)
- Numerator = number of patients who have a documented RASS score of -3 to +4 at any point this shift, who have had at least one CAM-ICU score documented since the beginning of this shift 
- Denominator = number of patients who have a documented RASS score of -3 to +4 at any point during this shift
- Calculation: (numerator / denominator)*100 represented as percentage
- 
  *Note the percentage does not include patients with a CAM-ICU score documented, but no RASS score documented.* 
  *it also does not include patients with a CAM-ICU score documented who have a RASS score of < -3.*
   
NOTE:
- there are no need for epochs for this calcualtion
- the denominator can potentially be a bigger number than the current number of patients occupying the ICU beds (allowing for admissions / discharges), hence representing this as percentage and not a fraction
- the following could potentially be excluded from the calculation:
a) RASS -4/-5 with a CAM-ICU score - this is theoretically possible to document (by accident) but highly unlikely
b) NO Valid RASS documented with a CAM-ICU score documented - this is possible as the bedside nurse may assume that a RASS score documented in the final hour of the last shift is still valid or incorrect as per clinical guidelines as RASS and CAM-ICU should be documented concurrently - both these scenarios are unlikely and would be even less likely once improvement work on thie metric is underway

**[B] CAM-ICU Percentage Completions Last Shift - Front Tile**
- get all flowsheet data for previous shift
-  then go through logic
- IF the current time falls between 08:00-19:59 (day shift), calculate the number of patients with at least 2 consecutive RASS scores of -3 to +4 during the previous shift (20:00 yesterday to 07:59 today)
-  IF the current time falls between 20:00-07:59 (night shift), calculate the number of patients with at least 2 consecutive RASS scores of
 of -3 to +4 during the previous shift, calculate the number who have at least one CAM-ICU score documented (positive or negative) during the previous shift 
- Numerator = number of patients with at least two consecutive RASS scores of -3 to +4 who have had at least one CAM-ICU score documented during the previous shift 
- Denominator = number of patients with at least two consecutive RASS scores of -3 to +4 during the previous shift 

*the following feeds into the (i) front tile - 24-hour rolling window and (ii) SPC patients with delirium chart*

**[C]  overall CAM-ICU front tile calculation: Patients with Delirium in the last 24 hours**

- Numerator: the number of patients with positive CAM-ICU scores in the last 24 hours 
- Denominator: the number of patients with at present on on each unit that have had a RASS score of -3 to +4 (at any point) in the last 24 hours

![image](https://github.com/inform-us/requirements_specifications/assets/167782531/e2b82308-a00b-45d6-a5fa-28b46eba09ea)

*The following feeds into the floorplans*

**[D] Floorplan labelling**
MAKE EPOCHS FOR THIS SECTION

1) If the latest (real or forward-filled) CAM-ICU score reading this shift= negative: ‘GREEN’; design = green filled bed
2) If the latest (real or forward-filled) CAM-ICU score reading this shift = positive: ‘RED’; design = red filled bed 
3) If there is no CAM-ICU score since the start of the shift (since 08:00 day or 20:00 night) ‘missing’: ‘missing’; design = white filled bed with red hashed outline
4) If the latest CAM-ICU score not applicable as RASS score has fallen to -4- -5: ‘assessment not required (RASS is -5 or -4)’ design = white filled bed with blue hashed outline (RASS pips CAM)
    - This logic is applied across all epochs, so we override the CAM-ICU score for a particular row if RASS falls below -3.
5) CAM-ICU with a null RASS - label as either: `positive with no RASS` or `negative with no RASS`

![image](https://github.com/inform-us/requirements_specifications/assets/167782531/1281d06f-09e7-42ca-9d60-c2c03701a970)

*The following feeds into the individual patient charts*

**[E] Classification Rules: Individual patient chart**
MAKE EPOCHS FOR THIS SECTION

1) X-axis time in hours, range 0-72 hours, default to 24 hours
2) Y-axis left is CAM-ICU score divided into 'Positive' at top and 'Negative' at bottom
3) CAM-ICU score: 'POSITIVE' = delirium is present, 'NEGATIVE: delirium is not present
4) Label all CAM-ICU scores as circles
5) Plot all positive CAM-ICU scores on top half of chart as red filled circle
6) Plot all negative CAM-ICU scores on bottom half of chart as green filled circle
7) 'Missing' CAM-ICU scores shown as grey vertical bar with no data points
8) CAM-ICU not required shown as grey tick on central dividing line

  ![image](https://github.com/inform-us/requirements_specifications/assets/167782531/69d62352-10e9-4a19-90eb-f37ec423304e)
 

---
# [F] SPC CHARTS -below is a working draft.... !

**CAM-ICU SPC CHARTS (refer to XYZ metric in classification**

1. A day shift is defined as 08:00-19:59 on one day
2. A night shift is defined as 20:00-07:59 on one day
3. Calendar day defined as 00:00 - 23:59
4. Shift week is defined as Monday 08:00 – Monday 07:59
5. There are fourteen shifts in every week
6. These charts are weekly percentage (p-charts)
  
## Chart 1a and 1b 1c [Patient chart] 
**Percentage of eligible patients with positive CAM-ICU scores (total combined shifts, day and night shifts)– weekly chart**

Operational definition = out of all patients with at least two consecutive RASS scores (or forward filled scores) of -3 to +4 what proportion of patients have at least one positive CAM-ICU score during day and night shifts on a weekly basis? 
## Chart 1a 
**Weekly Percentage of positive CAM-ICU scores all shifts**

## Chart 1b 
**Weekly Percentage of positive CAM-ICU scores (day shift)**
1. Break the week down into fourteen 12-hour shift epochs, seven 08:00-19:59 and seven 20:00-07:59. 
2. For each 12-hour day shift epoch (08:00-19:59), calculate the number of patients with at least two consecutive RASS scores of -3 to +4 at least one of which is in this shift
3. For each 12-hour day shift epoch, calculate the number of patients that have had at least one positive CAM-ICU score documented that shift
   - Numerator = number of patients that have had at least one positive CAM-ICU score documented each day shift
   - Denominator =  number of patients with at least two consecutive RASS scores of -3 to +4 one of which is in each day shift
5. Divide step 3 number by step 2 number. Denote as percentage. This is the shift's percentage of positive CAM-ICU scores (day shift)
6. Repeat steps 2-4 seven times for each 12-hour day shift epoch in the week
7. Sum all day shift percentages, divide by seven. Denote as percentage. This is the weekly percentage of positive CAM-ICU scores (day shift).
## Chart 1b 
**Weekly Percentage of positive CAM-ICU scores (night shift)**
1. For each 12-hour night shift epoch (20:00-07:59), calculate the number of patients with at least two consecutive RASS scores of -3 to +4, at least one of which is in this shift
3. For each every 12-hour night shift epoch, calculate the number of patients that have had at least one positive CAM-ICU score documented that shift
   - Numerator = number of patients that have had at least one positive CAM-ICU score documented each night shift
   - Denominator =  number of patients with at least two consecutive RASS scores of -3 to +4 
5. Divide step 3 number by step 2 number. Denote as percentage. This is the shift's percentage of positive CAM-ICU scores (night shift)
6. Repeat steps 2-4 seven times for each 12-hour night shift epoch in the week
7. Sum all night shift percentages, divide by seven. Denote as percentage. This is the average weekly percentage of positive CAM-ICU scores (night shift).

## Chart 2 [CAM-ICU documentation chart]
**Weekly percentage of CAM-ICU scores documented once per shift as per guidelines**

Operational definition = out of all patients with at least two consecutive RASS scores of -3 to +4, what proportion of these patients have at least one CAM-ICU documented per shift on a weekly basis?

1) Break the week down into fourteen 12-hour shift, seven 08:00-19:59 and seven 20:00-07:59. 
2) For each 12-hour day shift epoch (08:00-19:59), calculate the number of patients with at least two consecutive RASS scores of -3 to +4, at least one of which is in this shift
3) For each every 12-hour day shift epoch, calculate the number of patients that have had at least one positive CAM-ICU score documented that shift
4)  For each 12-hour night shift epoch (08:00-19:59), calculate the number of patients with at least two consecutive RASS scores of -3 to +4 at least one of which is in this shift
5)  For each every 12-hour night shift epoch, calculate the number of patients that have had at least one positive CAM-ICU score documented that shift
   -  Numerator = number of patients that have had at least one CAM-ICU score documented each shift
   -  Denominator =  number of patients with at least two consecutive RASS scores of -3 to +4 (eligible patients)
6)  Divide step 3 by step 2. Denote as percentage. This is the day shift's percentage of CAM-ICU scores documented
7)  Divide step  5 by step 4.  Denote as percentage. This is the night shift's percentage of CAM-ICU scores documented
8) Repeat fourteen times for each 12-hour shift 
9) Sum all fourteen shift percentages, divide by fourteen. Denote as percentage. This is the average weekly percentage of CAM-ICU scores documented




