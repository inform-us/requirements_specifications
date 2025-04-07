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

  |Flowsheet|Flowsheet Number| Manual/Automatic/Calculated Input | Comments|Expected documentation frequency|
  |-|-|-|-|-|
  |R CAM-ICU FEATURE 1: ACUTE ONSET OR FLUCTUATING COURSE|3040104645|Manual| Drop Down (free text possible)|Once between 0800-1959 and once between 2000-0759|
  |R CAM-ICU FEATURE 2: INATTENTION|3040104647|Manual| Drop Down (free text possible)|Once between 0800-1959 and once between 2000-0759|
  |R CAM-ICU FEATURE 3: ALTERED LEVEL OF CONSCIOUSNESS|3040104648|Calculated|Autopopulated when RASS score is entered|Hourly between 0800 - 1959. Four hourly between 2000 - 0759|
  |R CAM-ICU FEATURE 4: DISORGANIZED THINKING|3040104649|Manual| Drop Down (free text possible)|Once between 0800-1959 and once between 2000-0759. Note: Feature 4 is not required if feature 3 is positive|
  |R CAM-ICU OVERALL|3040104650|Calculated|Autopopulated from the flowsheets above|Once between 0800-1959 and once between 2000-0759|
  |R RICHMOND AGITATION SEDATION SCALE|3040104644|Manual|Drop Down (free text possible)|Hourly between 0800 - 1959. Four hourly between 2000 - 0759|
  
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
b) NO Valid RASS documented with a CAM-ICU score documented means that at the time of CAM-ICU documentation, the last RASS score documented has now surpassed its validity period and become expired (either it has been 1 hours and 15 minutes in the day or 4 hours and 15 minutes in the night). Ideally CAM-ICU and RASS should be documented concurrently as a concurrent RASS autofills one of the four CAM-ICU features, but this is not always done. Once improvement work on this metric is underway, this will be less likely. We will therefore need to denote when CAM-ICUs are documented without valid RASS score to prompt reviews of RASS on the floorplan. 

**[B] CAM-ICU Percentage Completions Last Shift - Front Tile**
- get all flowsheet data for previous shift
- Includes all patients from the previous shift (including discharged patients who were present during the previous shift)
- Numerator = number of patients who have a documented RASS score of -3 to +4 at any point the previous shift, who have had at least one CAM-ICU score documented during the previous shift
- Denominator = number of patients who have a documented RASS score of -3 to +4 at any point the previous shift
- Calculation: (numerator / denominator)*100 represented as percentage
  
*the following feeds into the (i) front tile - 24-hour rolling window and (ii) SPC patients with delirium chart*

**[C]  overall CAM-ICU front tile calculation: Patients with Delirium in the last 2 (completed) shifts**
- This is a live update that looks at incidence of delirium over the last 2 completed shifts (includes both inpatients and discharged patients).
- This calculation does not include the 'current' shift (i.e. the shift we are currently within) as we only want to consider fully 'completed' shifts. Therefore, the calculation will focus on the 2 fully completed shifts that have occurred prior to the 'current' shift.
  - The rationale for this is that only one assessment is required per shift, therefore an incomplete shift will not reflect the quantity of delirium on a ward accurately.
- Numerator: the number of patients present on each unit at any time over the last 2 completed shifts with at least one positive CAM-ICU score that is documented at any point over those shifts.
- Denominator: the number of patients present on each unit at any time over the last 2 completed shifts.
- Calculation: (numerator / denominator)*100 represented as percentage

![image](https://github.com/inform-us/requirements_specifications/assets/167782531/e2b82308-a00b-45d6-a5fa-28b46eba09ea)

*The following feeds into the floorplans*

**[D] Floorplan labelling**
MAKE EPOCHS FOR THIS SECTION

1) If the latest (real or forward-filled) CAM-ICU score reading this shift= negative: ‘GREEN’; design = green filled bed
2) If the latest (real or forward-filled) CAM-ICU score reading this shift = positive: ‘RED’; design = red filled bed
3) If the latest CAM-ICU score is positive, but the latest RASS is not within 75 minutes (06:00 - 21.59) or 4 hours and 15 minutes (22:00 - 05:59), label bed as CAM-ICU positive, RASS overdue.
4) If the latest CAM-ICU score is negative, but the latest RASS is not within 75 minutes (06:00 - 21.59) or 4 hours and 15 minutes (22:00 - 05:59), label bed as CAM-ICU positive, RASS overdue.  
5) If there is no CAM-ICU score since the start of the current shift (since 08:00 day or 20:00 night) ‘missing’: ‘missing’; design = white filled bed with red hashed outline
6) If the latest CAM-ICU score is not applicable as RASS score has fallen to -4- or -5: ‘assessment not required (RASS is -5 or -4)’ design = white filled bed with blue hashed outline (RASS pips CAM-ICU)
    - This logic is applied across all epochs, so we override the CAM-ICU score for a particular row if RASS falls below -3.

![image](https://github.com/inform-us/requirements_specifications/assets/167782531/1281d06f-09e7-42ca-9d60-c2c03701a970)

*The following feeds into the individual patient charts*

**[E] Classification Rules: Individual patient chart**
MAKE EPOCHS FOR THIS SECTION

1) X-axis time in hours, range 0-72 hours, default to 24 hours
2) Y-axis left is CAM-ICU score divided into 'Positive' at top and 'Negative' at bottom
3) CAM-ICU score: 'POSITIVE' = delirium is present, 'NEGATIVE: delirium is not present
4) Label all CAM-ICU scores as circles
5) Plot all positive CAM-ICU scores with a valid RASS on top half of chart as red filled circle
6) Plot all negative CAM-ICU scores with a valid RASS on bottom half of chart as green filled circle
7) Plot all positive CAM-ICU scores without a valid RASS on top half of chart as red hashed filled circle
8) Plot all negative CAM-ICU scores without a valid RASS on bottom half of chart as green hashed filled circle
8) 'Missing' CAM-ICU scores shown as grey vertical bar with no data points
9) CAM-ICU not required shown as grey tick on central dividing line

  ![image](https://github.com/inform-us/requirements_specifications/assets/167782531/69d62352-10e9-4a19-90eb-f37ec423304e)
 

---
# [F] SPC CHARTS

**CAM-ICU SPC CHARTS (refer to XYZ metric in classification)**

1. A day shift is defined as 08:00-19:59 on one day
2. A night shift is defined as 20:00-07:59 on one day
3. Calendar day defined as 00:00 - 23:59
5. There are fourteen shifts in every week
6. These charts are weekly percentage (p-charts)
  
## Chart 1a, 1b and  1c [Patient chart] - one SPC chart with three tabs (cf MAP, SpO2)
**Percentage of patients with positive CAM-ICU scores (1a total combined shifts, 1b day shifts and 1c night shifts) – weekly chart**

Operational definition = The percentage of patients that have had at least one positive CAM-ICU score (therefore a delirium diagnosis) during a calendar day OR per day / night shifts (on a weekly basis)

## Chart 1a 
**Weekly percentage of patients with a positive CAM-ICU score per CALENDAR DAY**

Calendar week is defined as Monday 00:00hrs to Sunday 23:59hrs. 

1. This looks at data on a calendar day basis (00:00 - 23:59)
3. Establish each patient present on each of the units for that calendar day (including current inpatients and those that have been discharged)
4. Identify for each of these patients whether there was a positive CAM-ICU score documented at any time during the calendar day
5. **Numerator** = number of patients that have had one (or more) positive CAM-ICU score(s) documented on each calendar day
6. **Denominator** = number of patients present on each calendar day (including current inpatients and those that have been discharged)
7. Calculate a daily percentage of positive CAM-ICU scores (delirium) = numerator / denominator 
8. Calculate aggregated weekly mean of the 7 calendar days (sum of percentage of each of the seven days / seven). Denote as percentage.
9.  SPC data point = weekly calendar day shift aggregated mean of numerator/denominator as percentage

### n-number for process limit calculation

The n-number for chart 1a is the weekly aggregated denominator from point 6 above.

**Tooltip display** = process limit n-number with the label "eligible patients".

> [!NOTE]
> This is correct in the code as of 2025-03-14 (though tooltip is hidden on prod)

## Chart 1b 
**Weekly percentage of patients with a positive CAM-ICU score during a DAY SHIFT**

 Shift week is defined as Monday 08:00 – Sunday 19:59

1. This looks at data on a day shift basis (08:00-19:59)
2. Establish each patient present on each of the units for the day shift (including current inpatients and those that have been discharged)
3. Idenifty for each of these patients whether there was a positive CAM-ICU score documented at any time during the day shift
4. **Numerator** = number of patients that have had one (or more) positive CAM-ICU score(s) documented on each day shift
5. **Denominator** = number of patients present on each day shift (including current inpatients and those that have been discharged)
6. Calculate a daily day shift percentage of positive CAM-ICU scores (delirium) = numerator / denominator 
7. Calculate the aggregated weekly mean of the 7 day shifts (sum of percentage of each of the seven day shifts / seven). Denote as percentage.
8.  SPC data point = weekly day shift aggregated mean of numerator/denominator as percentage

### n-number for process limit calculation

The n-number for chart 1b is the weekly aggregated denominator from point 5 above.

**Tooltip display** = process limit n-number with the label "eligible patients".

> [!NOTE]
> This is correct in the code as of 2025-03-14 (though tooltip is hidden on prod)


## Chart 1c 
**Weekly percentage of patients with a positive CAM-ICU score during a NIGHT SHIFT**

 Shift week is defined as Monday 20:00 Monday 07:59

1. This looks at data on a night shift basis (20:00-07:59)
2. Establish each patient present on each of the units for the night shift (including current inpatients and those that have been discharged)
3. Idenifty for each of these patients whether there was a positive CAM-ICU score documented at any time during the night shift
4. Numerator = number of patients that have had one (or more) positive CAM-ICU score(s) documented on each night shift
5. Denominator = number of patients present on each night shift (including current inpatients and those that have been discharged)
6. Calculate a daily night shift percentage of positive CAM-ICU scores (delirium) = numerator / denominator 
7. Calculate the aggregated weekly mean of the 7 night shifts (sum of percentage of each of the seven night shifts / seven). Denote as percentage.
8.  SPC data point = weekly night shift aggregated mean of numerator/denominator as percentage
9. NOTE - the night shift that starts on Sunday at 20:00 and ends Monday 07:59 is included in the data from the previous week (i.e. the week that ends the Sunday the night shift starts)


### n-number for process limit calculation

The n-number for chart 1c is the weekly aggregated denominator from point 5 above.

**Tooltip display** = process limit n-number with the label "eligible patients".

> [!NOTE]
> This is correct in the code as of 2025-03-14 (though tooltip is hidden on prod)




## Chart 2 [CAM-ICU documentation chart]
**Weekly percentage of CAM-ICU scores documented at least once per shift as per guidelines**

Operational definition = For all patients who are eligible for a CAM-ICU score (have documented RASS score of -3 to +4 meaning they are awake enough to be able to complete the assessment).
The proportion of CAM-ICU scores that have been documented at least once per shift (on a weekly basis).

Shift week is defined as Monday 08:00 – Monday 07:59. 

*This means the night shift that starts on Sunday at 20:00 and ends Monday 07:59 is included in the data from the previous week (i.e. the week that ends the Sunday the night shift starts).*

This looks at data on a per shift basis, which is then converted into a weekly percentage based on a shift week. 

Calculations should include all patients who were present for any time during each shift, including those who were discharged during that shift. 

1. Break the week down into fourteen 12-hour shifts, seven 08:00-19:59 and seven 20:00-07:59.
2. For each 12-hour shift, calculate the number of patients with a RASS score of -3 to +4 documented at least once at any point during the shift.
3. **Numerator** - patients present on each shift with at least one documented RASS score of -3 to +4 at any time during that shift AND at least one CAM-ICU score documented at any time during that shift (RASS and CAM-ICU do not have to be concurrent).
4. **Denominator** - all patients present each shift with at least one a RASS score of -3 to +4 documented during that shift.
5. Combine numerators from all of the shifts where there were patients present.
6. Combine denominators from all of the shifts where there were patients present.
7. SPC data point = weekly aggregated mean of numerator/denominator as percentage

### n-number for process limit calculation

The n-number for chart 2 is the combined denominator from point 6 above.

**Tooltip display** n-number with the label "denominator".

> [!NOTE]
> This is correct in the code as of 2025-03-14 (though tooltip is hidden and called "eigible patients")
