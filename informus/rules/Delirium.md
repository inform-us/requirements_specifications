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

  |Flowsheet|Flowsheet Number| Manual/Automatic/Calculated Input | Comments|
  |-|-|-|-|
  |R CAM-ICU FEATURE 1: ACUTE ONSET OR FLUCTUATING COURSE|3040104645|Manual| Drop Down (free text possible)|
  |R CAM-ICU FEATURE 2: INATTENTION|3040104647|Manual| Drop Down (free text possible)|
  |R CAM-ICU FEATURE 3: ALTERED LEVEL OF CONSCIOUSNESS|3040104648|Calculated|Autopopulated when RASS score is entered|
  |R CAM-ICU FEATURE 4: DISORGANIZED THINKING|3040104649|Manual| Drop Down (free text possible)|
  |R CAM-ICU OVERALL|3040104650|Calculated|Autopopulated from the flowsheets above|
  |R RICHMOND AGITATION SEDATION SCALE|3040104644|Manual|Drop Down (free text possible)|
  
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

*note If a patient has a RASS score of <-3 documented, CAM-ICU can still be generated on EPIC. Even though a CAM-ICU assessment is physcially immpossible when patient is this sedated* check

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
  *it also does not include patients with a CAM-ICU score documented who have a RASS score of < -3 documented.*
   
NOTE:
- there are no need for epochs for this calculation
- the denominator can potentially be a bigger number than the current number of patients occupying the ICU beds (allowing for admissions / discharges), hence representing this as percentage and not a fraction
- the following could potentially be excluded from the calculation:
a) RASS -4/-5 with a CAM-ICU score - this is theoretically possible to document (by accident) but highly unlikely
b) NO Valid RASS documented with a CAM-ICU score documented - this is possible as the bedside nurse may assume that a RASS score documented in the final hour of the last shift is still valid or incorrect as per clinical guidelines as RASS and CAM-ICU should be documented concurrently - both these scenarios are unlikely and would be even less likely once improvement work on this metric is underway

**[B] CAM-ICU Percentage Completions Last Shift - Front Tile**
- get all flowsheet data for previous shift
- Includes all patients from the previous shift (including discharged patients who were present during the previous shift)
- Numerator = number of patients who have a documented RASS score of -3 to +4 at any point the previous shift, who have had at least one CAM-ICU score documented during the previous shift
- Denominator = number of patients who have a documented RASS score of -3 to +4 at any point the previous shift
- Calculation: (numerator / denominator)*100 represented as percentage
  
*the following feeds into the (i) front tile - 24-hour rolling window and (ii) SPC patients with delirium chart*

**[C]  overall CAM-ICU front tile calculation: Patients with Delirium in the last 24 hours**
- This is a live update that looks at incidence of delirium in the last 24 hours (inpatients and those discharged)
- Refer to CAM-ICU validity rules above (use backfilled CAM-ICU) *even if the last CAM-ICU was documented over 24 hours ago, it was still valid until the end of that shift so should be included*
- Numerator: the number of patients present on on each unit at any time over the last 24 hours  with positive CAM-ICU scores in the last 24 hours 
- Denominator: the number of patients present on on each unit at any time over the last 24 hours 
- Calculation: (numerator / denominator)*100 represented as percentage

![image](https://github.com/inform-us/requirements_specifications/assets/167782531/e2b82308-a00b-45d6-a5fa-28b46eba09ea)

*The following feeds into the floorplans*

**[D] Floorplan labelling**
MAKE EPOCHS FOR THIS SECTION

1) If the latest (real or forward-filled) CAM-ICU score reading this shift= negative: ‘GREEN’; design = green filled bed
2) If the latest (real or forward-filled) CAM-ICU score reading this shift = positive: ‘RED’; design = red filled bed 
3) If there is no CAM-ICU score since the start of the shift (since 08:00 day or 20:00 night) ‘missing’: ‘missing’; design = white filled bed with red hashed outline
4) If the latest CAM-ICU score not applicable as RASS score has fallen to -4- or -5: ‘assessment not required (RASS is -5 or -4)’ design = white filled bed with blue hashed outline (RASS pips CAM-ICU)
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
5) Plot all positive CAM-ICU scores with a RASS on top half of chart as red filled circle
6) Plot all negative CAM-ICU scores with a RASS on bottom half of chart as green filled circle
7) Plot all positive CAM-ICU scores without a RASS on top half of chart as red hashed filled circle
8) Plot all negative CAM-ICU scores without a RASS on bottom half of chart as green hashed filled circle
8) 'Missing' CAM-ICU scores shown as grey vertical bar with no data points
9) CAM-ICU not required shown as grey tick on central dividing line

  ![image](https://github.com/inform-us/requirements_specifications/assets/167782531/69d62352-10e9-4a19-90eb-f37ec423304e)
 

---
# [F] SPC CHARTS

**CAM-ICU SPC CHARTS (refer to XYZ metric in classification)**

1. A day shift is defined as 08:00-19:59 on one day
2. A night shift is defined as 20:00-07:59 on one day
3. Calendar day defined as 00:00 - 23:59
4. Shift week is defined as Monday 08:00 – Monday 07:59
5. There are fourteen shifts in every week
6. These charts are weekly percentage (p-charts)
  
## Chart 1a, 1b and  1c [Patient chart] - one SPC chart with three tabs (cf MAP, SpO2)
**Percentage of patients with positive CAM-ICU scores (1a total combined shifts, 1b day shifts and 1c night shifts) – weekly chart**

Operational definition = out of all patients what proportion of patients have at least one positive CAM-ICU score during a calendar day OR per day / night shifts on a weekly basis? 

## Chart 1a 
**Weekly percentage of patients with a positive CAM-ICU score per CALENDAR DAY**

1. This looks at data on a calendar day basis (00:00 - 23:59)
2. Establish each patient present on each of the units for that calendar day (including current inpatients and those that have been discharged)
3. Idenifty for each of these patients whether there was a positive CAM-ICU score documented at any time during the calendar day
4. Numerator = number of patients that have had one (or more) positive CAM-ICU score(s) documented on each calendar day
   Denominator = number of patients present on each calenday day (including current inpatients and those that have been discharged)
5. Calculate a daily percentage of positive CAM-ICU scores (delirium) = numerator / denominator 
6. Calculate weekly mean of the 7 calendar days (sum of percentage of each of the seven days / seven). Denote as percentage. 

## Chart 1b 
**Weekly percentage of patients with a positive CAM-ICU score during a DAY SHIFT**

1. This looks at data on a day shift basis (08:00-19:59)
2. Establish each patient present on each of the units for the day shift (including current inpatients and those that have been discharged)
3. Idenifty for each of these patients whether there was a positive CAM-ICU score documented at any time during the day shift
4. Numerator = number of patients that have had one (or more) positive CAM-ICU score(s) documented on each day shift
   Denominator = number of patients present on each day shift (including current inpatients and those that have been discharged)
5. Calculate a daily day shift percentage of positive CAM-ICU scores (delirium) = numerator / denominator 
6. Calculate weekly mean of the 7 day shifts (sum of percentage of each of the seven day shifts / seven). Denote as percentage. 

## Chart 1c 
**Weekly percentage of patients with a positive CAM-ICU score during a NIGHT SHIFT**

1. This looks at data on a night shift basis (20:00-07:59)
2. Establish each patient present on each of the units for the night shift (including current inpatients and those that have been discharged)
3. Idenifty for each of these patients whether there was a positive CAM-ICU score documented at any time during the night shift
4. Numerator = number of patients that have had one (or more) positive CAM-ICU score(s) documented on each night shift
   Denominator = number of patients present on each night shift (including current inpatients and those that have been discharged)
5. Calculate a daily night shift percentage of positive CAM-ICU scores (delirium) = numerator / denominator 
6. Calculate weekly mean of the 7 night shifts (sum of percentage of each of the seven night shifts / seven). Denote as percentage.
7. NOTE - the night shift that starts on Sunday at 20:00 and ends Monday 07:59 is included in the data from the previous week (i.e. the week that ends the Sunday the night shift starts)
   - SHIFT WEEK is defined as Monday 08:00 – Monday 07:59
   - WE MAY NEED TO ALTER THE TIME OF THE WEEKLY SPC DATA CAPTURE FOR THE DELIRIUM SPC, WHICH NORMALLY OCCURS EVERY MONDAY AT 03:00/04:00, IT WOULD NEED TO HAPPEN AFTER THE END OF THE NIGHT SHIFT ON MONDAY MORNING 

## Chart 2 [CAM-ICU documentation chart]
**Weekly percentage of CAM-ICU scores documented at least once per shift as per guidelines**

Operational definition = out of all patients with a documented RASS score of -3 to +4, what proportion of these patients have at least one CAM-ICU documented per shift on a weekly basis?

1. This looks at data on a per shift basis, which is then converted into a weekly percentage based on a shift week (defined as Monday 08:00 – Monday 07:59)
2. Break the week down into fourteen 12-hour shift, seven 08:00-19:59 and seven 20:00-07:59
3. Note to include current inpatients and those that have been discharged for each shift

4. For each 12-hour day shift (08:00-19:59), calculate the number of patients with a RASS scores of -3 to +4, documented at least once during this shift
5. For these patients (that have a RASS -3 to +4 on the 12-hour day shift), calculate the number of patients that have had at least one positive CAM-ICU score documented during this shift
6. Calculate percentage CAM-ICU documented on day shift:
   Numerator - patients present on day shift with at least one RASS score of -3 to +4 AND at least one CAM-ICU score documented (does not have to be concurrent)
   Denominator - all patients present on day shift (including current inpatients and those that have been discharged for that shift)

7. For each 12-hour night shift (20:00-07:59), calculate the number of patients with a RASS scores of -3 to +4, documented at least once during this shift
8. For these patients (that have a RASS -3 to +4 on the 12-hour night shift), calculate the number of patients that have had at least one positive CAM-ICU score documented during this shift
9. Calculate percentage CAM-ICU documented on night shift:
   Numerator - patients present on night shift with at least one RASS score of -3 to +4 AND at least one CAM-ICU score documented (does not have to be concurrent)
   Denominator - all patients present on night shift (including current inpatients and those that have been discharged for that shift)

10. Take the percentges for the number of shifts that week (14 if a complete week) and generate a mean (sum of percentages of shifts / number of shifts), denote as a percentage - this is the shift week data point
11. NOTE - the night shift that starts on Sunday at 20:00 and ends Monday 07:59 is included in the data from the previous week (i.e. the week that ends the Sunday the night shift starts)
   - SHIFT WEEK is defined as Monday 08:00 – Monday 07:59
   - WE MAY NEED TO ALTER THE TIME OF THE WEEKLY SPC DATA CAPTURE FOR THE DELIRIUM SPC, WHICH NORMALLY OCCURS EVERY MONDAY AT 03:00/04:00, IT WOULD NEED TO HAPPEN AFTER THE END OF THE NIGHT SHIFT ON MONDAY MORNING 
