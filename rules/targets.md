|File .md signed_off|Code review|Production|Outstanding|
|---|---|---|---|
|yes - 09/05/24|- pending code review <br> - Y/N to alternate SPC (line 116)|no|- remove references to daily targets in MD file (line 87) <br> - adjust content from daily to weekly|

# Target Rules
Rules for all targets set metric

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

- the 8 physiological metrics are independent of each other, but for the 'all targets set' metric to be met, ALL the 8 physiological targets need to have had an entry made within the designated time frame (see below)
- the 'all targets set' metric has a binary output: (1) SET (all targets set within time frame) or (2) NOT SET
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

1. For the purposes of the 'all targets set' metric, each of the **_individual_** 8 physiological metrics returns a binary response: <br> (1) [individual_SET] - any of the set range or number / not applicable / other (comment) / free text entry are returned (an entry generating a _dt stamp), or <br> (2) [individual_NOT SET] nothing is returned (no entry and therefore no _dt stamp)
2. Each of the 8 physiological metrics can be superseded if an entry is updated or new entry is made, this will generate a new _dt stamp (more recent) and become the 'valid' entry
3. Each of the 8 physiological metrics is valid from when the _dt stamp is set, until 07:59 hours, after which point they become invalid, from 08:00 onwards all of these 8 physiological targets need to be set afresh (i.e  can only be valid for a maximum time of 24 hours between the hours of [current day] 08:00 - [next day] 07:59)
4. In order to meet the 'all targets set' metric (SET), **ALL** 8 physiological metrics need to have been returned with a valid _dt stamp <br> i.e. **ALL** 8 physiological metrics return an [individual_SET] within the time frame of [current day] 08:00 - [next day] 07:59


## CLASSIFICATION 

**[A] Proportion of patients with 'all targets set'**

Feeds into (i) front tile (current time snapshot), (ii) floorplan and (iii) 'all targets set' SPC chart

**FRONT TILE proportion of patients with 'all targets set'**
1. The front tile displays live data (i.e. the current state on each unit)
2. For each patient ALL of the 8 physiological targets need to have been completed in the ICU Targets section of the ICU Navigators (i.e. a valid _dt stamp for an entry for each individual metric) in order to achive (1) SET; if any of the 8 physiological metrics is missing an entry (a valid _dt stamp) then return (2) NOT SET
3. Numerator = sum of patients achieving (1) SET response
4. Denominator = total number of current patients (occupied beds)
5. For each unit this is displayed as a fraction (numerator / denominator); except on T03 where the unit is divided into 15-bed Northside (beds 1-16 (no bed 13)) & 20-bed Southside (beds 17-36), displaying a proportion for each side

**[B] Floorplan labelling
1. The floorplan displays live data (current state) on a bed by bed basis and is updated as new data is available (outcome is binary and there is no option for 'missing data')
2. If 'all targets set'; design = green filled bed
3. If 'all targets not set'; design = red filled bed
4. If bed is empty; design = white filled bed with dark grey outline

**There is no individual chart for the 'all targets set' metric**

---
## SPC CHART

**Relevant SPC chart information**

**_PLEASE NOTE SPC CHART CURRENTLY GENERATING DAILY DATA - DELETE THIS LINE & ADJUST FRONT END TEXT ONCE ZENHUB TICKETS 891 & 1113 resolved_**

1. This is a weekly percentage (p-chart) SPC
2. It differs from the other SPC charts in that it takes a snapshot at 13:00, and not a calendar day aggregate
3. Week defined as Monday 00:00 – Sunday 23:59
4. 'Working clinical day' (24 hours) defined as [current day] 08:00 - [next day] 07:59 - labeled as the day of the week at the start of the 24 hour period (e.g. Sunday date xx/xx/xxxx 08:00 until Monday date +1/xx/xxxx 07:59 calculation performed on Monday, but labeled a 'Sunday' working clinical day) - **_ONLY RELEVANT TO ALTERNATE SPC 'CALENDAR DAY VERSION'_**

**ALL TARGETS SET IN ICU NAVIGATOR**

Proportion of 'all targets set' in ICU navigators

Operational definition = of documented physiological targets set in ICU Navigators in EPIC, what proportion of all patients have all their targets set by 13:00 each day on a weekly basis?  

1. Metric compliance is measured at 13:00 on each day, for the purposes of this SPC calculation, the code is set to run at 13:30 to give small amount of leeway for a clinically busy day
2. For each patient ALL of the 8 physiological targets need to have been completed in the ICU Targets section of the ICU Navigators (i.e. a valid _dt stamp for an entry for each individual metric) in order to achieve (1) SET; if any of the 8 physiological metrics is missing an entry (a valid _dt stamp) then return (2) NOT SET
3. Numerator = sum of patients achieving (1) SET response
4. Denominator = total number of current patients (occupied beds) at 13:30 hours
5. Calculate daily percentage for each unit, (exceptionally) treating T03 as Northside & Southside (e.g. T03N, T03S, T06, GWB & WMS units)
6. Aggregate the daily percentages into a **-weekly mean percentage_** for each of these respective units (T06, GWB & WMS)
7. Aggregate the daily percentages into a **_weekly mean percentage_** for T03 Northside & T03 Southside producing one value for the unit T03
8. Plot an SPC chart for each respective unit: y-axis = weekly percentage; x-axis = time

**NOTE**
- this SPC chart has an alternative design for the purposes of adding a competitive edge (gamify) to the daily clinical working pattern
- a consequence of this method (i.e. snapshot versus calendar day) is that a small proportion of patients may not be accounted for, specifically those admitted after 13:00 and discharged before 13:00 the next day: (i) severely ill and early death (ii) straightforward unplanned admission and quick discharge (iii) straightforward elective surgery and quick discharge.
- group (iii) is most likely to affect T06 (surgical patients) if patient flow is working well, but conversely these may be the least likely to benefit clinically from target setting
- an alternative SPC calculation is proposed below to ascertain complexity from developer perspective and if uncomplicated could generate a second SPC chart

---
**ALTERNATE - ALL TARGETS SET IN ICU NAVIGATOR - CALENDAR DAY VERSION**

Proportion of 'all targets set' in ICU navigators

Operational definition = of documented physiological targets set in ICU Navigators in EPIC, what proportion of all patients have all their targets set each 'working clinical day' on a weekly basis?  

1. Metric compliance is measured for the preceding 'working clinical day' and includes all patients present on a unit from 07:59 on the day of the calculation to 08:00 the day before; the calculation date label should be for the day before (e.g. Sunday date xx/xx/xxxx 08:00 until Monday date +1/xx/xxxx 07:59 calculation performed on Monday, but labeled a 'Sunday working clinical day') 
2. Identify all patients present on each unit during the 'working clinical day' (this will be the denominator)
3. For each patient ALL of the 8 physiological targets need to have been completed within the 24 hour period of a clinical working day in the ICU Targets section of the ICU Navigators (i.e. a valid _dt stamp for an entry for each individual metric) in order to achieve (1) SET; if any of the 8 physiological metrics is missing an entry (a valid _dt stamp) then return (2) NOT SET
4. Numerator = sum of patients achieving (1) SET response
5. Denominator = total number of patients present on each unit during the working clinical day
6. Using the working clinical day definition (see above - day label), calculate daily percentage for each unit, (exceptionally) treating T03 as Northside & Southside (e.g. T03N, T03S, T06, GWB & WMS units)
8. Aggregate the daily percentages into a **-weekly mean percentage_** for each of these units (T06, GWB & WMS)
9. Aggregate the daily percentages into a **-weekly mean percentage_** for T03 Northside & T03 Southside producing one value for the unit T03
10. Plot an SPC chart for each respective unit: y-axis = weekly percentage; x-axis = time
