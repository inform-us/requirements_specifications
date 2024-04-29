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
7. Fluid Balance (fluid balance target to achieve by end of calendar day (UNIT = ml, integer)) - options: (i) set target number; (ii) not applicable; (iii) other (comment) +/- free text entry
8. RASS (Richmond Agitation Sedation Score (UNIT = nil; 10 point scale (-5 to +4))) - options: (i) set target number; (ii) not applicable; (iii) other (comment) +/- free text entry

- the 8 physiological metrics are independent of each other, but for the 'all target set' metric to be met, ALL the 8 physiological targets need to have had an entry made within the designated time frame (vide infra)
- the 'all target set' metric has a binary output: (1) SET (all targets set within time frame) or (2) NOT SET
- there are no corresponding targets for this metric

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

* ### Miscellaneous information:
- not used - Row ID	- R UCLH ICU READY DISCHARGE [41222]
- there are no components to form a summative score

---

---
[TARGETS_user interface sequence .pdf](https://github.com/inform-us/requirements_specifications/files/15090740/TARGETS_frontend.sequence.pdf)

## ELIGIBILITY 

1. All patients across all units


## VALIDITY up to 24 hour time window - (floorplan & SPC)

1. For the purposes of the 'all target set' metric, each of the 8 physiological metrics returns a binary response: (1) [SET] - any of the set range or number / not applicable / other (comment) / free text entry are returned (all generating a _dt stamp), or (2) [NOT SET] nothing is returned.
2. Each of the 8 physiological metrics can be superseded if an entry is updated or new entry is made, this will generate a new _dt stamp (more recent) and become the 'valid' entry
3. Each of the 8 physiological metrics is valid from _dt stamp it is set, until 07:59 hours, after which point they become invalid, from 08:00 onwards all of these 8 physiological targets need to be set afresh (i.e  can only be valid for a maximum time of 24 hours between the hours of 08:00 - 07:59)
4. In order to meet the 'all target set' metric, all 8 physiological metrics need to have been returned with a valid _dt stamp


## CLASSIFICATION 

**[A] Proportion of patients with 'all target set'**

Feeds into (i) front tile (current time snapshoot), (ii) floorplan and (iii) 'all target set' SPC chart

**FRONT TILE proportion of patients with 'all target set'**
1. The front tile displays live data (i.e. the current state on each unit)
2. For each patient ALL of the 8 physiological targets need to have been completed in the ICU Targets section of the ICU Navigators (i.e. a valid _dt stamp for an entry for each individual metric) in order to achive (1) SET; if any of the 8 physiological metrics is missing an entry (a valid _dt stamp) then return (2) NOT SET
3. Numerator = sum of patinets achieving (1) SET response
4. Denominator = total number of current patients (occupied beds)


---
# SPC CHARTS 
## TARGETS SET - Daily percentage of all targets set in ICU navigators 
Operational definition= what proportion of all patients have all their targets set in ICU navigators in EPIC by 1pm each day?  

1. Generate percentage of patients with all 8 (Spo2, MAP, RASS, pH, haemoglobin, fluid balance, paCO2, paO2) daily - i.e. add up number of patients with all targets set at 1pm and divide by number of patients on unit at that time 
2. Present as percentage
3. Plot on daily chart

3. Compliance measured at 13:00 hours each day 

 
