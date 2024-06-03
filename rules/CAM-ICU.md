# CAM-ICU Delirium 
Rules for CAM-ICU Metric

## EPIC
- CAM-ICU metric is a binary score
- The score is required on all patients that have at least two consecutive RASS scores of -3 to +4 during any 12-hour shift.
- The two possible outcomes for CAM-ICU score are positive or negative.
- A positive score denotes that a patient has delirium, a negative score denotes that a patient does not have delirium. 
- There are no targets for these variables, however we endeavour clinically to have as few positive scores as we can. 

## EPIC Flowsheets
 - overall CAM-ICU- Row ID 3040104650
-  Richmond Agitation Sedation Scale (RASS)- Row ID 3040104644

---

---
PDF - ABC metric user interface sequence 

## ELIGIBILITY 

- All patients who have had at least two consecutive RASS scores of -3 to +4 this shift

## VALIDITY
1) The CAM-ICU metric should be documented once per 12-hour shift
2) 12-hour shifts are defined as 08:00-19:59 (day shift) and 20:00-07:59 (night shift)
3) Every CAM-ICU score set on a day shift (between 08:00-19:59) is valid until 20:00 hours or until a subsequent score is documented. 
4) Every CAM-ICU score set on a night shift (between 20:00-07:59) is valid until 08:00or until a subsequent score is documented. 
5) Each CAM-ICU score therefore expires at 08:00 and 20:00 every day. 
6) Each documented CAM-ICU score can be superseded if an entry is updated or new entry is made during that shift, this will generate a new _dt stamp (more recent) and become the 'valid' entry

## CLASSIFICATION 

*The following data feeds into (i) the text at the bottom of the CAM-ICU front tile and (ii) SPC CAM-ICU documentation chart*

**[A] CAM-ICU Percentage Completions This Shift Front Tile**

  - calculate the number of patients with at least two consecutive RASS scores of -3 to +4 this shift (since 08:00 hours or 20:00 hours today) 
- for each patient with at least two consecutive RASS scores of -3 to +4 this shift, calculate the number who have at least one CAM-ICU score documented (positive or negative) this shift (since 08:00 hours or 20:00 hours today) 
- Numerator = number of patients with at least 2 consecutive RASS scores of -3 to +4 who have had at least one CAM-ICU score documented since the beginning of this shift 
- Denominator = number of patients with at least 2 consecutive RASS scores of -3 to +4 this shift (since 08:00 hours or 20:00 hours today)
  
**[B] CAM-ICU Percentage Completions Last Shift Front Tile**
- IF the current time falls between 08:00-19:59 (day shift), calculate the number of patients with at least 2 consecutive RASS scores of -3 to +4 during the previous shift (20:00 yesterday to 07:59 today)
-  IF the current time falls between 20:00-07:59 (night shift), calculate the number of patients with at least 2 consecutive RASS scores of
 of -3 to +4 during the previous shift, calculate the number who have at least one CAM-ICU score documented (positive or negative) during the previous shift 
- Numerator = number of patients with at least two consecutive RASS scores of -3 to +4 who have had at least one CAM-ICU score documented during the previous shift 
- Denominator = number of patients with at least two consecutive RASS scores of -3 to +4 during the previous shift 

*the following feeds into the (i) front tile - 24-hour rolling window and (ii) SPC patients with delirium chart*

**[B]  overall CAM-ICU front tile calculation: Patients with Delirium in the last 24 hours**


- calculate the number of patients with at least two consecutive RASS scores of -3 to +4 in the last 24 hours
- calculate the number of patients with at least one positive CAM-ICU in the last 24 hours 
- Numerator: the number of patients with positive CAM-ICU scores in the last 24 hours 
- Denominator: the number of patients with at least two consecutive RASS scores of -3 to +4 in the last 24 hours



![image](https://github.com/inform-us/requirements_specifications/assets/167782531/e2b82308-a00b-45d6-a5fa-28b46eba09ea)

*The following feeds into the floorplans*
**[C] Floorplan labelling**

1) If latest CAM-ICU score reading this shift= negative: ‘GREEN’; design = green filled bed 
2) If latest CAM-ICU score reading this shift = positive: ‘RED’; design = red filled bed 
3) If there is no CAM-ICU score since the start of the shift (since 08:00 day or 20:00 night)  ‘missing’: ‘missing’; design = white filled bed with red hashed outline
4) If latest CAM-ICU score not applicable as RASS score has fallen to -4- -5: ‘assessment not required (RASS is -5 or -4)’ design = white filled bed with blue hashed outline

![image](https://github.com/inform-us/requirements_specifications/assets/167782531/1281d06f-09e7-42ca-9d60-c2c03701a970)

*The following feeds into the individual patient charts*

**[D] Classification Rules: Individual patient chart**


1) X-axis time in hours, range 0-72 hours, default to 24 hours
2) Y-axis left is CAM-ICU score divided into 'Positive' at top and 'Negative' at bottom
3) CAM-ICU score: 'POSITIVE' = delirium is present, 'NEGATIVE: delirium is not present
4) Label all CAM-ICU scores as circles
5) Plot all positive CAM-ICU scores on top half of chart as red filled circle
6) Plot all negative CAM-ICU scores on bottom half of chart as green filled circle
7) 'Missing' CAM-ICU scores shown as grey vertical bar with no data points
8) CAM-ICU not required shown as grey tick on central dividing line 

![image](https://github.com/inform-us/requirements_specifications/assets/167782531/cf4c8747-a8c1-40d4-971c-65a22ca4e4bf)

---
# [E] SPC CHARTS -below is a working draft.... !

**CAM-ICU SPC CHARTS (refer to XYZ metric in classification**

1. A day shift is defined as 08:00-19:59 on one day
2. A night shift is defined as 20:00-07:59 on one day
3. Calendar day defined as 00:00 - 23:59
4. Shift week is defined as Monday 08:00 – Monday 07:59
5. There are fourteen shifts in every week
6. These charts are weekly percentage (p-charts)
  
## Chart 1a and 1b [Patient chart] 
**Proportion of eligible patients with positive CAM-ICU scores (day and night shifts)– weekly chart**

Operational definition = out of all patients with at least two consecutive RASS scores of -3 to +4 in a shift what proportion of patients have at least one positive CAM-ICU score on a weekly basis? 

1. Break the week down into fourteen 12-hour shift epochs, seven 08:00-19:59 and seven 20:00-07:59. 
2. For every 12-hour day shift epoch (08:00-19:59), calculate the number of patients with at least two consecutive RASS scores of -3 to +4 in the shift epoch
3. For each of these patients, calculate the number that have had at least one positive CAM-ICU score documented
4. Repeat seven times for each 12-hour day shift epoch
5. Numerator= number of patients with at least one positive CAM-ICU score documented per each shift epoch
6. Denominator= number of patients with at least two consecutive RASS scores of -3 to +4 per each shift epoch
7. Sum seven numerators
8. Sum seven denominators
9. Denote as percentage

   
## Chart 2 [CAM-ICU documentation chart]
**Proportion of CAM-ICU scores done once per shift as per guidelines**

Operational definition = out of all patients with at least two consecutive RASS scores of -3 to +4 in a shift, what proportion of these patients have at least one CAM-ICU documented per shift?

1) Break the week down into fourteen 12-hour shift epochs, seven 08:00-19:59 and seven 20:00-07:59. 
2. For every 12-hour day shift epoch (08:00-19:59), calculate the number of patients with at least two consecutive RASS scores of -3 to +4 in the shift epoch
3. For each of these patients, calculate the number that have had at least one CAM-ICU score documented
4. Repeat seven times for each 12-hour day shift epoch
5. Numerator= number of patients with at least one CAM-ICU score documented per each shift epoch
6. Denominator= number of patients with at least two consecutive RASS scores of -3 to +4 per each shift epoch
7. Sum seven numerators
8. Sum seven denominators
9. Denote as percentage


1. These are weekly percentage (p-charts) SPC

