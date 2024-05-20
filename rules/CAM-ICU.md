# CAM-ICU Delirium 
Rules for CAM-ICU Metric

## EPIC
- general information about metric (e.g. location, components, group or summative score etc)
- metric output (e.g. numerical (integer / decimal), drop down, range selection, free text etc)
- Are there corresponding targets?
xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx

## EPIC Flowsheets
* ### ABC metric [ID XXXX for Group or summative score if applicable]
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
4) Every  CAM-ICU score set on a night shift (between 20:00-07:59) is valid until 08:00or until a subsequent score is documented. 
5) Each CAM-ICU score therefore expires at 08:00 and 20:00 every day. 
6) Each documented CAM-ICU score can be superseded if an entry is updated or new entry is made during that shift, this will generate a new _dt stamp (more recent) and become the 'valid' entry

## CLASSIFICATION 

*The following data feeds into (i) the text at the bottom of the CAM-ICU front tile and (ii) SPC CAM-ICU documentation chart*

**[A] CAM-ICU Percentage Completions This Shift Front Tile**
  - calculate the number of patients with at least two consecutive RASS scores of -3 to +4 this shift (since 08:00 hours or 20:00 hours today) 
- for each patient with at least two consecutive RASS scores of -3 to +4 this shift, calculate the number who have at least one CAM-ICU score documented (positive or negative) this shift (since 08:00 hours or 20:00 hours today) 
- Numerator = number of patients with at least 2 consecutive RASS scores of -3 to +4 who have had at least one CAM-ICU score documented since the beginning of this shift 
- Denominator = number of patients with at least 2 consecutive RASS scores of -3 to +4 this shift (since 08:00 hours or 20:00 hours today) 
**[A] CAM-ICU Percentage Completions Last Shift Front Tile**
- IF the current time falls between 08:00-19:59 (day shift), calculate the number of patients with at least 2 consecutive RASS scores of -3 to +4 during the previous shift (20:00 yesterday to 07:59 today)
-  IF the current time falls between 20:00-07:59 (night shift), calculate the number of patients with at least 2 consecutive RASS scores of
 of -3 to +4 during the previous shift, calculate the number who have at least one CAM-ICU score documented (positive or negative) during the previous shift 
- Numerator = number of patients with at least two consecutive RASS scores of -3 to +4 who have had at least one CAM-ICU score documented during the previous shift 
- Denominator = number of patients with at least two consecutive RASS scores of -3 to +4 during the previous shift 

*the following feeds into the (i) front tile - 24-hour rolling window and (ii) SPC patients with delirium chart*

**[B]  overall CAM-ICU front tile calculation: Patients with Delirium in the last 24 hours**

- calculate the number of patients with at least two consecutive RASS scores of -3 to +4 in the last 24 hours
- calculate the number of patients with at least one positive CAM-ICU in the last 24 hours 
-numerator: the number of patients with positive CAM-ICU scores in the last 24 hours 
-denominator: the number of patients with at least two consecutive RASS scores of -3 to +4 in the last 24 hours

*The following feeds into the floorplans*

**[C] Floorplan labelling**
1) If latest CAM-ICU score reading this shift= negative: ‘GREEN’; design = green filled bed 
2) If latest CAM-ICU score reading this shift = positive: ‘RED’; design = red filled bed 
3) If there is no CAM-ICU score since the start of the shift (since 08:00 day or 20:00 night)  ‘missing’: ‘missing’; design = white filled bed with red hashed outline
4) If latest CAM-ICU score not applicable as RASS score has fallen to -4- -5: ‘assessment not required (RASS is -5 or -4)’ design = white filled bed with blue hashed outline

*The following feeds into the individual patient charts*

**[D] Classification Rules: Individual patient chart**


---
# [E] SPC CHARTS 

**ABC SPC CHARTS (refer to XYZ metric in classification**

1. Calendar day defined as 00:00 - 23:59
2. Week defined as Monday 00:00 – Sunday 23:59
  
## Chart 1 [Patient chart] 
**Proportion of moderate or severe pain scores – weekly chart**

Operational definition = of the documented pain scores in EPIC, what proportion are moderate or severe on a weekly basis? 

   
**Chart 2**

1. These are weekly percentage (p-charts) SPC
2. Week defined a Monday 00:00 – Sunday 23:59
