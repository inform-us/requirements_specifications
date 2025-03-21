# TIDAL VOLUME rules
Rules for Tidal volume metric

 ## EPIC Flowsheets


* ### Individual metric Row ID:
| Flowsheet | Row ID | Manual/Automatic/Calculated Input | Comments | Expected documentation frequency|
  |-|-|-|-|-|
  |O2 delivery|3040109305|Manual| Drop down (free text available)| Hourly (varies depending on patient's clinical condition)|
  |Vent Mode|3040102607|Manual| Drop down (free text available)|  Hourly (varies depending on patient's clinical condition)|
  |Tidal Volume||from monitor||

  ## Eligibility Rules (patient is on mandatory ventilation)
 1)  All patients on mandatory ventilation 
  2) If O2 delivery mode has 'tracheostomy' or 'endotrachael' entered and if valid O2 delivery is set patient is_intubated
 4)  If Vent mode is VC, PC PRVC, PPV, SIMV, PRVC, APRV, then ventmode is mandatory. Patient is on mandatory ventilation
 5)  All must be true in order for patient to be on mandatory ventilation.
    

## Validity (time window) Rules: 

1) O2 delivery only valid if o2delivery_dt within last 6 hours of epoch 
2) Vent mode score only valid if vent_mode_vt_dt within last 6 hours of epoch_dt
3) Tidal Volume validity is 4 hours and 15 minutes to give leeway 

## Summary Rules (corresponds to tile metric) 
Exclude missing, off unit, or not applicable. Take mean of ventmode value- display as number with one decimal point. 
Total hours on mandatory ventiliation = eligible hours, exclude missing, off unit, or not applicable

## Classification Rules: (corresponds to the per patient chart) 

   1. IF not 'is_ventilated':'not applicable'
   2. IF not 'has_valid_vent_mode_vt': 'missing' 
   3. IF 'vent_mode_vt' 10.0:  'out_of_range_10' (out of range) 
   4. IF 'vent_mode_vt' > 8.0: 'out_of_range_8' (out of range) 
   5. IF s['vent_mode_vt'] <= 8.0: 'in range' 
   6. IF none of the above 'fallthrough' 

## Labelling Rule: (corresponds to the floor plans)     

  1. IF the latest classification is 'not applicable':'not applicable' 
  2. IF the latest classification is 'missing': 'missing' 
  3. IF latest 3 or more readings are 'out_of_range_8':'out of range' 
  4. IF latest 2 or more readings are 'out_of_range_10':'out of range' 
  5. IF there are 5 or more non-consecutive 'out_of_range_8' in 24 hours:'out of range'
  6. IF the latest classification is 'in range': 'in range'
  7. Insert extra rules to avoid fallthrough cases from code review here.
  8.  IF none of the above: 'fallthrough'
*n.b. fallthrough is shown as dark grey bed on floorplan, but there is no accompanying legend item. This is explained to user in ? button.*
 ---    

# SPC CHARTS 

## NOTE

Calendar week defined as: Monday 00:00 - Sunday 23:59:59

Eligible patients: only patients who meet eligibility rules above (i.e on mandatory ventilation / O2 delivery mode has 'tracheostomy' or 'endotrachael' entered / valid O2 delivery is set patient is_intubated / if Vent mode is VC, PC PRVC, PPV, SIMV, PRVC, APRV (ventmode is mandatory).

Data required: (i) number of eligible patients (ie. CSN that meet above criteria); (ii) 1-hour epoch labels (in range / all 'out of range')

##  Tidal Volume- Weekly percentage of patients achieving Tidal Volume target (<8ml/kg IBW)

Operational definition = of the patients who are intubated and on mandatory ventilation, what proportion are achieving their tidal volume target, i.e. < or = 8ml/kg IBW on a weekly basis?

### 1 HOUR EPOCHS & DISCARD ‘IN’-ELIGIBLE HOURS 
1. 1-hour epochs from labelling rules above
2. Discard the following epoch labels:
     - ‘n/a’ (not on mandatory ventilation and therefore not eligible to be in this metric calculation)
     - 'missing'
     - ‘fall through’
     - ‘not set’ (no target set)
3. Include all labels that are out of range and those that are in range:
     -  'out of range'
     -  'in range'

### Percentage calculation
1. Fetch data from the previous calendar week
2. Find the number of eligible patients (see note above) for each unit
3. Find the corresponding hourly epoch labels for each individual patient (only labels are: 'out of range' and ' in range' within that calendar week

4. IN RANGE
- **Numerator** = count of the number of 1-hour epochs labelled as 'in range' (for each eligible patient - CSN)
- **Denominator** = count of the number of 1-hour epochs labelled as 'in range' and 'out of range’ (for each eligible patient - CSN)
- Calculate the individual eligible patient (CSN) percentage for the calendar week = numerator / denominator
- Aggregate all the weekly patient percentages and divide by the number of patients who contributed to above calculation to generate an **aggregated weekly percentage mean** of 'the proportion of patients achieving (in range) their tidal volume target - **this is the SPC data point**
- Plot an SPC chart for: y-axis = weekly percentage; x-axis = time

5. Repeat for each respective unit T03/GWB/T06/WMS

8. SPC title would need to be adjusted to 'Weekly percentage DURATION of patients Tidal Volume below 8ml/kg IBW (patients on mandatory ventilation)
 
### n-number for process limits

n = number of eligible patients (point 2 above) who who contributed to above calculation on each respective unit during that week

**Tooltip display = process limit n-number and labelled as 'eligible patients' 

> [!NOTE]
