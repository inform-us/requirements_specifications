# RASS rules
Some description here...
## Validity (time window) Rules: 

## Classification Rules: (corresponds to the per patient chart) 

1. if 'is_ventilated' : 'not applicable' 
2. Add is_sedated check when drugs available 
3. if 'has_valid_rass': missing' 
4. if 'has_valid_numerical_rass_target': 'below target' , 'above target', 'on target' 
5. if 'has_valid_entered_rass_target'] :'non-numerical' 
6. if non of the above rules: 'not set' 
