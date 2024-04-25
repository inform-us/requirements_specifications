# Target Rules
Rules for all target set metric

## EPIC
- ICU targets are set in the 'ICU Navigators' tab [doctors log in view] and are then displayed in the flowsheet 'ICU targets' tab
- there are currently 8 physiological variables:
1. MAP (mean arterial blood pressure (UNIT = mmHg; integer)) - options: (i) set range; (ii) not applicable; (iii) other (comment) +/- free text entry
2. SpO2 (saturation pulse oximeter (UNIT = %; integer)) - options: (i) set range; (ii) not applicable; (iii) other (comment) +/- free text entry
3. PaO2 (arterial partial pressure of oxygen (UNIT = kPa; decimal)) - options: (i) set range; (ii) not applicable; (iii) other (comment) +/- free text entry
4. PaCO2 (arterial partial pressure of carbon dioxide (UNIT = kPa; decimal)) - options: (i) set range; (ii) not applicable; (iii) other (comment) +/- free text entry
5. pH (power hydrogen (UNIT = nil; (log) decimal)) - options: (i) set range; (ii) not applicable; (iii) other (comment) +/- free text entry
6. Haemoglobin (blood haemoglobin concentration (UNIT = g/l; integer)) - options: (i) set range; (ii) not applicable; (iii) other (comment) +/- free text entry
7. Fluid Balance (fluid balance to achieved by end of calendar day (UNIT = ml, decimal rounded to whole number)) - options: (i) set target number; (ii) not applicable; (iii) other (comment) +/- free text entry
8. RASS (Richmond Agitation Sedation Score (UNIT = nil; integer)) - options: (i) set target number; (ii) not applicable; (iii) other (comment) +/- free text entry

- general information about metric (e.g. location, components, group or summative score etc)
- metric output (e.g. numerical (integer / decimal), drop down, range selection, free text etc)
- Are there corresponds targets?

[TARGETS_user interface sequence .pdf](https://github.com/inform-us/requirements_specifications/files/15090740/TARGETS_frontend.sequence.pdf)

## EPIC Flowsheets

* ### Group ID:
- G UCLH ICU TARGETS [36552] 

* ### Individual metric Row ID:
1. MAP - R UCLH ICU TARGET MAP [36554]
2. SpO2 - R UCLH ICU TARGETS SPO2 [36551]	
3. PaO2 - R UCLH ICU TARGET PAO2 [36556]
4. PaCO2	- R UCLH ICU TARGET PACO2 [36557]
5. pH -	R UCLH ICU TARGETS PH [36559]
6. Haemoglobin - R UCLH ICU TARGET HB [36558]
7. Fluid Balance - R UCLH ICU TARGETS FLUID BALANCE [36553]
8. RASS - R UCLH ICU TARGET RASS [36555]

Miscellaneous information:
- not used - Row ID	- R UCLH ICU READY DISCHARGE [41222]
- there are no components to for a summative score

---
## ELIGIBILITY 

1. All patients across all units

## VALIDITY (time window)

## CLASSIFICATION 
1. All eight physiological targets completed in the ICU Targets section of the ICU Navigators
2. Compliance measured at 13:00 hours each day 

---
# SPC CHARTS 
## TARGETS SET - Daily percentage of all targets set in ICU navigators 
Operational definition= what proportion of all patients have all their targets set in ICU navigators in EPIC by 1pm each day?  

1. Generate percentage of patients with all 8 (Spo2, MAP, RASS, pH, haemoglobin, fluid balance, paCO2, paO2) daily - i.e. add up number of patients with all targets set at 1pm and divide by number of patients on unit at that time 
2. Present as percentage
3. Plot on daily chart

 
