# Mean Arterial Blood Pressure (MAP) rules
## Validity (time window) Rules: 

1. MAP only valid if map_dt within last 6 hours of epoch_dt 
2. Inotropes only valid if within last 4 hours 
3. 8:00 - 12:00 MAP Target Validity rule: 
-  if epoch time before 12noon, 
-  if map_target_dt after 8am on the day before then mark as valid else as invalid 
-  if epoch after 12noon, 
-  if map_target_dt after 8am on the morning of then mark as valid else as invalid 

        	 

 

Classification Rules: (corresponds to the per patient chart) 

    1) if not 'on_inotrope': 'not applicable' 

2) if not 'has_valid_map':'missing' 

3) if 'has_valid_numerical_map_target': below or above or in range 

4) if 'has_valid_entered_map_target':'non-numerical 

5) if non of the above 'not set' 

 

     

 

Labelling Rule: (corresponds to the floor plans)     

    1. if the latest 3 consecutive hours are all classified as 'above' then label patient as 'above' 

    2. if the latest 2 consecutive hours are both classified as 'below' then label patient as 'below'       

    3. if the latest classification is 'not applicable' then label the patient as 'not applicable' 

    4. if there are 5 non-consecutive hours in the 24hr timeseries classified as *either* 'below' or 'above', count backward and label the patient the majority label 

    5. if the latest hour is classified as 'in range', then label patient as 'in range' 

    6. if the latest classification is 'non-numerical' then label the patient as 'non-numerical' 

    7. if the latest classification is 'missing' then label the patient as 'missing' 

    8. if the latest classification is 'not set' then label the patient as 'not set' 

    9. if the classification was 'in range' and is now above(below) for fewer than 3(2) hours then label as 'in range' 

    10. if none of the rules matched then label the patient as 'fallthrough' 
