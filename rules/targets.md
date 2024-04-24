# Target Rules
Rules for all target set metric

## EPIC
- ICU targets are set in the 'ICU Navigators' tab [doctors log in view] and are then displayed in the flowsheet 'ICU targets' tab
- there are currently 8 physiological variables:
1. MAP (mean arterial blood pressure (UNIT = mmHg; integer)) - options: (i) set range; (ii) not applicable; (iii) other (comment) +/- free text entry
2. SpO2 (saturation pulse oximeter (UNIT = %; integer)) - options: (i) set range; (ii) not applicable; (iii) other (comment) +/- free text entry
3. PaO2 (arterial partial pressure of oxygen (UNIT = kPa; decimal)) - options: (i) set range; (ii) not applicable; (iii) other (comment) +/- free text entry
4. PaCO2 (arterial partial pressure of carbon dioxide (UNIT = kPa; decimal)) - options: (i) set range; (ii) not applicable; (iii) other (comment) +/- free text entry

- general information about metric (e.g. location, components, group or summative score etc)
- metric output (e.g. numerical (integer / decimal), drop down, range selection, free text etc)
- Are there corresponds targets?

## EPIC Flowsheets
* ### ABC metric [ID XXXX for Group or summative score if applicable]
 - ABC metric - Row ID XXXX
-  ABC metric [component if applicable] - Row ID XXXX

[TARGETS_frontend sequence .pdf](https://github.com/inform-us/requirements_specifications/files/15090740/TARGETS_frontend.sequence.pdf)

Group ID - G UCLH ICU TARGETS [36552] 

Row ID - R UCLH ICU TARGET MAP [36554]

Row ID - R UCLH ICU TARGETS SPO2 [36551]	

Row ID	- R UCLH ICU TARGET PAO2 [36556]

Row ID	- R UCLH ICU TARGET PACO2 [36557]

Row ID -	R UCLH ICU TARGETS PH [36559]

Row ID	- R UCLH ICU TARGET HB [36558]

Row ID	- R UCLH ICU TARGETS FLUID BALANCE [36553]

Row ID	- R UCLH ICU TARGET RASS [36555]

Row ID	- R UCLH ICU READY DISCHARGE [41222]





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

 
