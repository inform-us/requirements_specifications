# TIDAL VOLUME rules
Some description here...
 

## Validity (time window) Rules: 

1) O2delivery only valid if o2delivery_dt within last 6 hours of epoch 
2) Vent mode score only valid if vent_mode_vt_dt within last 4 hours of epoch_dt 



## Classification Rules: (corresponds to the per patient chart) 

   1. if not 'is_ventilated':'not applicable'
   2. if not 'has_valid_vent_mode_vt': 'missing' 
   3. if 'vent_mode_vt' 10.0:  'out_of_range_10' (out of range) 
   4. if 'vent_mode_vt' > 8.0: 'out_of_range_8' (out of range) 
   5. if s['vent_mode_vt'] <= 8.0: 'in range' 
   6. if none of the above 'fallthrough' 

## Labelling Rule: (corresponds to the floor plans)     

  1. if the latest classification is 'not applicable':'not applicable' 
  2. if the latest classification is 'missing' : 'out of range' 
  3. if latest 3 readings are 'out_of_range_8':'out of range' 
  4. if latest 2 readings are 'out_of_range_10':'out of range' 
  5. if there are 5 non consecutive 'out_of_range_8':'out of range' 
  6. if the latest classification is 'in range' : 'in range'
  7. if none of the above: 'fallthrough'
 ---    
# SPC CHARTS
##  Tidal Volume- Graph 8- Weekly percentage of patients exceeding/above/not achieving Tidal Volume target of 6-8ml/kg IBW 
Operational definition = of the patients who are intubated and on mandatory ventilation (modes), what proportion are exceeding their tidal volume target [i.e. >8ml/kg IBW] (‘above target’) on a weekly basis?

### GROUP PATIENT HOURLY DATA INTO CALENDAR DAY  
1. Group patient (MRN/CSN) hourly data into a calendar day

### GENERATE LABEL FOR 1 HOUR EPOCH & DISCARD ‘IN’-ELIGIBLE EPOCHS 
2. If more than one tidal volume reading in a one hour epoch, take last reading and discard others 
3. Discard the following hour epoch labels:
      -  ‘n/a’ (not intubated / mandatory ventilation mode)
      -  ‘fall through’
      -  ‘Missing’ 
