# Exemplar Metrics Inform_us Data Rules

### These are the data rules and thresholds for the metrics that appear on the inform_us dashboard https://informus.org.uk and are also ICU exemplar ward Power BI dashboards

## Pain 

### Flowsheets used 

Verbal Pain Scale (at rest)	3040104280

Verbal Pain Scale (at movement)	3040104281

CRITICAL CARE PAIN OBSERVATION SCORE	3040104659

### Patient Group

All patients in CCU

### PAIN SCORES

Denominator = All documented CPOT and VPS scores

Numerator = All documented CPOT and VPS scores that are none or mild

Inform_us displays this data in real time and also as weekly SPC chart showing the percentage of pain scores that are none or mild. 

Week defined a Monday 00:00 – Sunday 23:59.

### PAIN SCORE DOCUMENTATION 


Pain scores are considered 'on time' if they are documented within 1 hour and 15 minutes (added documentation leeway) after a moderate to very severe score. Otherwise the score is shown as missing. 

Pain scores are considered 'on time if they are documented within 4 hours and 15 minutes (added documentation leeway) after a none or mild score. Otherwise the score is shown as missing. 

Inform_us displays this data in real time and also as weekly SPC chart showing the percentage of pain scores are done 'on time' as per guidelines. 
Week defined a Monday 00:00 – Sunday 23:59.

## RASS 

### Flowsheets used


FiO2%	301550	

O2 delivery device	3040109305

Vent mode	3040102607

RASS score	3040104644

RASS target	36555

On admission

CLONIDINE	12351

FENTANYL	331223

PROPOFOL	331218	

MIDAZOLAM	3040101274

MORPHINE	331228

DEXMEDETOMIDINE	3040101250

### Patient Group

Patient is defined as sedated and mechanically ventilated if 

(i) on mandatory ventilation if O2 delivery 040109305 equals endotrachael tube or tracheostomy

(ii) ventmode 3040102607 equals CPAP/PS 

(iii) receiving sedative drugs (see flowsheets above) within the last 6 hours 


### RASS SCORES on TARGET

The percentage of documented RASS scores that are the same as the target set by the doctors

Numerator = documented RASS scores within target for sedated and ventilated patients 

Denominator = all documented RASS scores with an associated valid RASS target set for sedated and ventilated patients 

Inform_us displays this data in real time and also as weekly SPC chart showing the percentage of  RASS scores on target. 


### RASS SCORE DOCUMENTATION 

RASS documentation is expected one hourly during the day (06:00-21:59)and 4 hourly during the night (22:00-05:59).

RASS scores are considered 'on time' if they are documented within 1 hour and 15 minutes (added documentation leeway) during the DAY (06:00-21:59).  Otherwise the score is shown as missing. 

RASS scores are considered 'on time' if they are documented within 4 hours and 15 minutes (added documentation leeway) during the  NIGHT (22:00-05:59).  

Inform_us displays this data in real time and also as two weekly SPC charts (day and night) showing the percentage of pain scores are done 'on time' as per guidelines. 

To reflect the sedation guidelines defining day as different than 'shift day', e.g. 08:00-19:59, the week is defined as Monday 06:15 to Sunday 22:14 to (also allows for 15 minutes leeway). 


## CAM-ICU Delirium

### Flowsheets used

### Patient Group

All patients with a RASS score of -3 to +4 

### CAM-ICU SCORES

### CAM-ICU DOCUMENTATION


## Airway

### Flowsheets used

### Patient Group

All patients

### AIRWAY PLAN DOCUMENTED

### TYPE OF AIRWAY AND TURNING PLAN/DARRT CALL 


## DrEaMING

### Flowsheets used

### Patient Group

All patients on PACU (T06 and WMS) 

### DrEaMING STATUS 

### DrEAMING DOCUMENTATION 




