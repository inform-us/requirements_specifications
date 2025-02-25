# TIDAL VOLUME rules
Rules for Tidal volume metric

 ## EPIC Flowsheets


* ### Individual metric Row ID:
| Flowsheet | Row ID | Manual/Automatic/Calculated Input | Comments | Expected documentation frequency|
  |-|-|-|-|-|
  |O2 delivery|3040109305|Manual| Drop down (free text available)| Hourly (varies depending on patient's clinical condition)|
  |Vent Mode|3040102607|Manual| Drop down (free text available)|  Hourly (varies depending on patient's clinical condition)|
  |Tidal Volume||from monitor||

  ## Eligibility Rules (patient is on mandatory ventilation)
 1)  All patients on mandatory ventilation 
  2) If O2 delivery mode has 'tracheostomy' or 'endotrachael' entered and if valid O2 delivery is set patient is_intubated
 4)  If Vent mode is VC, PC PRVC, PPV, SIMV, PRVC, APRV, then ventmode is mandatory. Patient is on mandatory ventilation
 5)  All must be true in order for patient to be on mandatory ventilation.
    

## Validity (time window) Rules: 

1) O2 delivery only valid if o2delivery_dt within last 6 hours of epoch 
2) Vent mode score only valid if vent_mode_vt_dt within last 6 hours of epoch_dt
3) Tidal Volume validity is 4 hours and 15 minutes to give leeway 

## Summary Rules (corresponds to tile metric) 
Exclude missing, off unit, or not applicable. Take mean of ventmode value- display as number with one decimal point. 
Total hours on mandatory ventiliation = eligible hours, exclude missing, off unit, or not applicable

## Classification Rules: (corresponds to the per patient chart) 

   1. IF not 'is_ventilated':'not applicable'
   2. IF not 'has_valid_vent_mode_vt': 'missing' 
   3. IF 'vent_mode_vt' 10.0:  'out_of_range_10' (out of range) 
   4. IF 'vent_mode_vt' > 8.0: 'out_of_range_8' (out of range) 
   5. IF s['vent_mode_vt'] <= 8.0: 'in range' 
   6. IF none of the above 'fallthrough' 

## Labelling Rule: (corresponds to the floor plans)     

  1. IF the latest classification is 'not applicable':'not applicable' 
  2. IF the latest classification is 'missing': 'missing' 
  3. IF latest 3 or more readings are 'out_of_range_8':'out of range' 
  4. IF latest 2 or more readings are 'out_of_range_10':'out of range' 
  5. IF there are 5 or more non-consecutive 'out_of_range_8' in 24 hours:'out of range'
  6. IF the latest classification is 'in range': 'in range'
  7. Insert extra rules to avoid fallthrough cases from code review here.
  8.  IF none of the above: 'fallthrough'
*n.b. fallthrough is shown as dark grey bed on floorplan, but there is no accompanying legend item. This is explained to user in ? button.*
 ---    
# SPC CHARTS 

##  Tidal Volume- Weekly percentage of patients achieving Tidal Volume target of 6-8ml/kg IBW 
Operational definition = of the patients who are intubated and on mandatory ventilation (modes), what proportion are achieving their tidal volume target, i.e. < or = 8ml/kg IBW on a weekly basis?

### GROUP PATIENT HOURLY DATA INTO CALENDAR DAY  
1. Group patient (MRN/CSN) hourly data into a calendar day

### GENERATE LABEL FOR 1 HOUR EPOCH & DISCARD ‘IN’-ELIGIBLE EPOCHS 
2. IF more than one tidal volume reading in a one hour epoch, take last reading and discard others 
3. Discard the following hour epoch labels:
      -  ‘n/a’ (not intubated / mandatory ventilation mode)
      -  ‘fall through’
      -  ‘Missing’

### GENERATE DESIGNATION FOR PATIENT CALENDAR DAY 
4. Perform a count of the number of eligible hours in that calendar day (labels: ‘achieving target’ or ‘above target’). This is the denominator 
5. Take most frequent epoch count as the calendar day designation. IF highest count on that calendar day is ‘achieving target’ then designate as ‘achieving target’
6. IF highest count on that calendar day is ‘above target’ then designate as ‘above target’.  
7. IF the most frequent hour counts are equal (between ‘acheiving target’ and ‘above target' then calendar day designation = ‘achieving target’

### GENERATE DATA POINT FOR SPC CHART   
7. Take all of the patient calendar day designations and aggregate into one week: Week defined as: Monday 00:00 - Sunday 23:59 
8. Generate percentage achieving weekly tidal volume target (i.e. add up all ‘achieving target’ in that week and divide by ‘achieving target’ + ‘above target’ in that week). Present as percentage
9. Plot on weekly chart
