# Exemplar Metrics Inform_us Data Rules

### These are the data rules and thresholds for the metrics that appear on the inform_us dashboard https://informus.org.uk and are also ICU exemplar ward Power BI dashboards

Tip: cross-reference these data rules with the visual dashboard. 

## Targets Set

### Flowsheets used 

MAP - R UCLH ICU TARGET MAP [36554]

SpO2 - R UCLH ICU TARGETS SPO2 [36551]

PaO2 - R UCLH ICU TARGET PAO2 [36556]

PaCO2 - R UCLH ICU TARGET PACO2 [36557]

pH - R UCLH ICU TARGETS PH [36559]

Haemoglobin - R UCLH ICU TARGET HB [36558]

Fluid Balance - R UCLH ICU TARGETS FLUID BALANCE [36553]

RASS - R UCLH ICU TARGET RASS [36555]

### Patient Group

All patients in CCU

### TARGETS SET

The proportion of patients for whom all 8 physiological targets are set (or documented as not applicable) in ICU navigators between start of shift 08:00am and before 13:00hrs each day. 


Denominator = All patients present on the unit between 08:00am and 13:00hrs.

Numerator = All  patients with all 8 targets set 08:00am and 13:30hrs (30 minutes added for documentation leeway). 

Inform_us displays this data in real time and also as weekly SPC chart showing the percentage of patients with all targets set each day.

Week defined a Monday 00:00 – Sunday 23:59.


## Pain 

### Flowsheets used 

Verbal Pain Scale (at rest)	3040104280

Verbal Pain Scale (at movement)	3040104281

CRITICAL CARE PAIN OBSERVATION SCORE	3040104659

### Patient Group

All patients in CCU

### PAIN SCORES

A pain score is categorised as moderate or severe if the latest score is either 1) CPOT 3-8 or 2) VPS at move or at rest 2-4. 

Denominator = All documented CPOT and VPS scores

Numerator = All documented CPOT and VPS scores that are moderate or severe

Inform_us displays this data in real time and also as weekly SPC chart showing the percentage of pain scores that are moderate or severe. 

Week defined a Monday 00:00 – Sunday 23:59.

### PAIN SCORE DOCUMENTATION 


Pain scores are considered 'on time' if they are documented within 1 hour and 15 minutes (added documentation leeway) after a moderate to very severe score. Otherwise the score is shown as missing. 

Pain scores are considered 'on time if they are documented within 4 hours and 15 minutes (added documentation leeway) after a none or mild score. Otherwise the score is shown as missing. 


Denominator = number of pain scores 

Numerator = number of pain scores that are done within the guidelines 

Inform_us displays this data in real time and also as two weekly SPC charts (moderate/severe chart) and (none/mild chart) showing the percentage of pain scores are done 'on time' as per guidelines. 

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

R CAM-ICU OVERALL	3040104650
R RICHMOND AGITATION SEDATION SCALE	3040104644

### Patient Group

All patients with a RASS score of -3 to +4. 

*n.b. Includes all patients present on the unit during the current shift (including discharged patients who were present during this shift* 


### CAM-ICU SCORES

The percentage of patients with a positive CAM-ICU score. 

Numerator: the number of patients present on each unit at any time over the last 24 hours with at least one positive CAM-ICU score
Denominator: the number of patients present on each unit at any time over the last 24 hours

Inform_us displays this data in real time and also as 3 weekly SPC chart showing the (1. daily, 2. day shift, and 3. nightshift) rates of delirium as a weekly percentage. 

### CAM-ICU DOCUMENTATION

For Patients with a RASS of -3 to +4, CAM-ICU documentation is expected once per shift or if a person's mental state changes. 


Denominator = number of patients who have a documented RASS score of -3 to +4 at any point during this shift

Numerator = number of patients who have a documented RASS score of -3 to +4 at any point this shift, who have had at least one CAM-ICU score documented since the beginning of this shift

Inform_us displays this data as 'last shift' and 'this shift' and also as two weekly SPC charts (day and night) showing the percentage of pain scores are done 'on time' as per guidelines. 

Shift week is defined as Monday 08:00 – Monday 07:59

## Airway

### Flowsheets used

Airway	R UCLH ICU AIRWAY PLAN 24499
DAS Generic Airway Plan	R UCLH ICU AIRWAY PLAN DAS 24498
Plan A	R UCLH ICU AIRWAY PLAN A 23865
Emergency Teams	R UCLH ICU AIRWAY PLAN TRACHE CALL 24504
O2 delivery device	R OXYGEN DELIVERY METHOD 3040109305

### Patient Group

All patients

### AIRWAY PLAN DOCUMENTED

The proportion of patients who have had an ICU airway plan (flowsheet 24499 and either DAS Generic 24498 or Pan A 23865) documented since admission.

DENOMINATOR = total number of current number of inpatients on each unit 

NUMERATOR = current number of patients designated as COMPLETED 

Inform_us displays this data in real time and also as weekly SPC percentage charts. 



## Mobilsation (as part of DrEaMing bundle)


### Flowsheets used

Mobisation Achieved	40705

Reasons for not mobilising	47371

### Patient Group

All patients on PACU (T06 and WMS) 

### MOBILITY SCALE

Mobilisation is reported as part of the DrEaMing bundle and not as a stand alone metric

Last documented mobility scale and reasons for not mobilising (if not) is displayed in real time on inform_us. 






