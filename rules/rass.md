# RASS rules
Rules for RASS Sedation metric
## Validity (time window) Rules: 
1. O2 delivery only valid if o2delivery_dt within last 6 hours of epoch 
2. RASS score only valid if rass_dt within last 4 hours of epoch_dt 
3. 8:00 - 12:00 RASS Target Validity rule 


## Classification Rules: (corresponds to the per patient chart) 

1. if 'is_ventilated' : 'not applicable' 
2. Add is_sedated check when drugs available 
3. if 'has_valid_rass': missing' 
4. if 'has_valid_numerical_rass_target': 'below target' , 'above target', 'on target' 
5. if 'has_valid_entered_rass_target'] :'non-numerical' 
6. if non of the above rules: 'not set'

## Labelling Rule: (corresponds to the floor plans)     

1. if latest reading 'on target':'on target' 
2. if latest reading 'above target':'off target' 
3. if latest reading 'below target':'off target' 
4. if latest reading 'missing':'missing' 
5. if latest reading 'not set':'not set' 
6. if latest reading 'not applicable': 'not applicable' 
7. if latest reading 'non-numerical':'non-numerical' 
8. if none of the above: 'fallthrough' 
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
8. NOT ACHIEVING RASS TARGET CHART: calendar day designation = ‘not achieving target’ divided by all calendar day designations ‘achieving target’ + ‘not achieving target’ (i.e. add up all ‘not achieving target’ in that week and divide by ‘not achieving target’ + ‘achieving target’ in that week). Present as percentage

 

 
   
               
    
