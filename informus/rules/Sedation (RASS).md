|File .md signed_off|Code review|Production|Outstanding|
|---|---|---|---|
|no - 01/01/01|- pending code review|no|- abc <br> - def|

# SEDATION SCORE (using the Richmond Agitation Sedation Score -RASS) rules

Rules for Sedation (on mechanical ventilation) metric, measured using the RASS scale (sedation/agitation)

## EPIC
- The degree of sedation and conversely agitation are measured by the Richmond Agitation Sedation Score (RASS)
- For the purposes of the RASS metric tile, we are particularly interested in oversedation on mechanical ventilation (i.e. a score more negative than the target set) which has a detrimental impact on length of stay, morbidity & mortality, hence the eligibility criteria include 'is_ventilated' & 'is_sedated')
- RASS runs on 10 point scale from (agitated) +4/+3/+2/+1/0/-1/-2/-3/-4/-5 (sedated) - *see table below*
- RASS scale value is an integer (note EPIC will allow free text!)
- RASS expected charting frequency differs during the day and night: <br> RASS_frequency_DAY: day defined as 06:00:00 - 21:59:59 - hourly as per guideline <br> RASS_frequency_NIGHT: night defined as 22:00:00 - 05:59:59 - 4 hourly as per guideline
- Individual patient RASS target is set on a daily basis [see targets.md](./targets.md#ELIGIBILITY)
- The function of the SEDATION_metric is twofold: <br> (1) measurement interval - a RASS charting frequency within guidleines <br> (2) achieving set RASS target

___
**The Richmond Agitation Sedation Score**
|Description|Term|Score|
|---|---|---|
|Overtly combative or violent; immediate danger to staff|Combative|+4|
|Pulls on or removes tube(s) or catheter(s) or has aggressive behavior toward staff|Very agitated|+3|
|Frequent nonpurposeful movement or patient–ventilator dyssynchrony|Agitated|+2|
|Anxious or apprehensive but movements not aggressive or vigorous|Restless|+1|
|Spontaneously pays attention to caregiver|Alert and calm|0|
|Not fully alert, but has sustained (more than 10 seconds) awakening, with eye contact, to voice|Drowsy|-1|
|Briefly (less than 10 seconds) awakens with eye contact to voice|Light sedation|-2|
|Any movement (but no eye contact) to voice|Moderate sedation|-3|
|No response to voice, but any movement to physical stimulation|Deep sedation|-4|
|No response to voice or physical stimulation|Unarousable|-5|
___

## EPIC Flowshets 

### Ventilation flowsheet


FIO2_% 301550?
02 Flow rate r ip flowrate 500690?

   "o2delivery": "3040109305",
    "vent_mode": "3040102607",
    "rass_score": "3040104644",
    "rass_target": "36555",
    "CLONIDINE": "12351",
    "FENTANYL": "331223",
    "PROPOFOL": "331218",
    "MIDAZOLAM": "3040101274",
    "MORPHINE": "331228",
    "DEXMEDETOMIDINE": "3040101250"
    
### Group ID Richmond Agitation Sedation Scale (RASS)
- G UCLH ICU NEW NEUROLOGY [39859]

### Row ID RASS
- R RICHMOND AGITATION SEDATION SCALE (RASS) [3040104644]

[SEDATION_user interface sequence .pdf](https://github.com/inform-us/requirements_specifications/files/15480198/SEDATION_user.interface.sequence.pdf)

## ELIGIBILITY
1. Patient (i) on mandatory mechanical ventilation AND (ii) receiving sedative drugs within the last 6 hours

   (i)
3. If O2 delivery is endotrachael tube or tracheostomy, patient is on mandatory mechanical ventilation
4. If ventmode is CPAP/PS...., patient is on mandatory mechanical ventilation
5. Note in code we seem to be missing the step of classifying what is mandatory ventilation and what is not. we think ventmode set flowsheet. 
6. (ii)
7. if sedative volume flowsheet is any number (any charted volume), then the patient is sedated. If sedation volume flowsheet is NaN, then patient is not sedated. *note this should be backfilled from 4 hours and looks like current code it isn't*

## Validity (time window) Rules: 
1. O2 delivery device only valid if o2delivery_dt documented within last 6 hours of epoch
2. This is double checked with ventmode flowsheet
3. 
4.*Need to write validity rules here as original code was written with 8 hour leeway. note all early metrics may have extended leeway.* 

### RASS
- clinical guideline recommended charting frequency for RASS differs depending on time of day
- in line with other documentation we add 15 minutes leeway to the validity of the documented score to allow for clinical leeway

### RASS generate 
1) RASS scores documented between 06:00 - 21.59 is valid for 75 minutes
2) RASS scores documented between 22:00 - 05:59 is valid 255 minutes (4 hours & 15 minutes)
   *note current rules have same one hour rule for all day and night*
   

## Classification Rules: 
RASS Target set on any day is valid until 12:00hrs the day after the RASS target is set unless another target is set between 08:00 and 12:00hr on the second day. 

1. if 'is_ventilated': 'not applicable' 
2. Add is_sedated check when drugs available 
3. if 'has_valid_rass': missing' 
4. if 'has_valid_numerical_rass_target': 'below target', 'above target', 'on target' 
5. if 'has_valid_entered_rass_target']:'non-numerical' 
6. if non of the above rules: 'not set'

Note if two measurements, take most recent. 



## Labelling Rule: (corresponds to the floor plans)     

1. if latest reading 'on target':'on target' 
2. if latest reading 'above target':'off target' 
3. if latest reading 'below target':'off target' 
4. if latest reading 'missing':'missing' 
5. if latest reading 'not set':'not set' 
6. if latest reading 'not applicable': 'not applicable' 
7. if latest reading 'non-numerical':'non-numerical' 
8. if none of the above: 'fallthrough'
9. n.b. fallthrough is shown as dark grey bed on floorplan, but there is no accompanying legend item. This is explained to user in ? button.

    
---
# SPC CHARTS 
## RASS- Weekly percentage RASS target compliance
Operational definition = of the patients who are ventilated and on sedative drug therapy and have had RASS targets set in ICU navigators in EPIC, what proportion are achieving (‘on’) or not achieving (‘off’) the set RASS target on a weekly basis? 

### GROUP PATIENT HOURLY DATA INTO CALENDAR DAY
1. Group patient (MRN/CSN) hourly data into a calendar day

### GENERATE LABEL FOR 1 HOUR EPOCH & DISCARD ‘IN’-ELIGIBLE EPOCHS 
2. If more than one RASS reading in a one hour epoch, take last reading and discard others 

3. Discard the following hour epoch labels:
    - ‘n/a’ (not ventilated / sedated)
    - ‘fall through’
    - ‘not set’
    - ‘missing’
  
  ### GENERATE DESIGNATION FOR PATIENT CALENDAR DAY 
4. Perform a count of the number of eligible hours in that calendar day (labels: ‘on target’ or ‘off target’). This is the denominator
5. Take most frequent epoch count as the calendar day designation. IF highest count on that calendar day is ‘on target’ then designate as ‘on target’
6. IF highest count on that calendar day is ‘off target’ then designate as ‘off target’
7. IF the most frequent hour counts are equal (between ‘on target’ and ‘off target’ then calendar day designation = ‘on target’

### GENERATE DATA POINT FOR SPC CHART 
7. Take all of the patient calendar day designations and aggregate into one week: Week defined as: Monday 00:00 - Sunday 23:59 
9. Generate weekly percentage designations that are on target (i.e. add up all ‘on target’ in that week and divide by ‘on target’ + ‘off target’ in that week). Present as percentage
10. Plot on weekly chart

 

 
   
               
    
