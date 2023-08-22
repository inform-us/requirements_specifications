# RASS rules
Some description here...
## Validity (time window) Rules: 
1. O2delivery only valid if o2delivery_dt within last 6 hours of epoch 
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
