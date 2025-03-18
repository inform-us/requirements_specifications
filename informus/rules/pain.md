

# Pain rules
Rules for pain metric

## EPIC
- There will only be two pain scores (in EPIC) going forward
  - Verbal pain score - scale 0-4
  - Critical Care Pain Observation Tool (CPOT) - scale 0-8
- Pain scale value is an integer (EPIC will allow free text!)
- There are no targets for these variables

## EPIC Flowsheets

| Flowsheet| Row ID| Manual/Automatic/Calculated Input | Comments |Expected Documentation Frequency|
|-|-|-|-|-|
|Verbal Pain Scale (at rest) | 3040104280 | Manual | Drop down (free text possible) |Four hourly if previous score was 0 or 1 or unable to access, hourly if previous score was 2 or above|
|Verbal Pain Scale (at movement) | 3040104281 | Manual |  Drop down (free text possible) |Four hourly if previous score was 0 or 1 or unable to access, hourly if previous score was 2 or above|
|Facial Expression | 3040104654 | Manual |  Drop down (free text possible) |Four hourly if previous Critical Care Pain Observation Score score was 0 - 2, hourly if previous Critical Care Pain Observation Score score was 3 or above|
|Body Movements | 3040104655 | Manual |  Drop down (free text possible) |Four hourly if previous Critical Care Pain Observation Score score was 0 - 2, hourly if previous Critical Care Pain Observation Score score was 3 or above|
|Compliance with Ventilator | 3040104656 | Manual |  Drop down (free text possible) |Four hourly if previous Critical Care Pain Observation Score score was 0 - 2, hourly if previous Critical Care Pain Observation Score score was 3 or above|
|Vocalization (extubated patients)| 3040104657 | Manual |  Drop down (free text possible) |Four hourly if previous Critical Care Pain Observation Score score was 0 - 2, hourly if previous Critical Care Pain Observation Score score was 3 or above|
|Muscle Tension| 3040104658 | Manual |  Drop down (free text possible) |Four hourly if previous Critical Care Pain Observation Score score was 0 - 2, hourly if previous Critical Care Pain Observation Score score was 3 or above|
|CRITICAL CARE PAIN OBSERVATION SCORE| 3040104659 | Calculated | Entry calculated from manual inputs above |Four hourly if previous score was 0 or 2, hourly if previous score was 3 or above|

* ### Verbal Pain Scale (VPS)
 - VERBAL PAIN SCALE (at rest) - Row ID 3040104280
 - VERBAL PAIN SCALE (at movement) - Row ID 3040104281

* ### Critical Care Pain Observation Tool (CPOT) - components
- Facial Expression - Row ID 3040104654
- Body Movements - Row ID 3040104655 
- Compliance with Ventilator - Row ID 3040104656
- OR
- Vocalization (extubated patients) - Row ID 3040104657
- Muscle Tension - Row ID 3040104658
 
- CRITICAL CARE PAIN OBSERVATION SCORE - Row ID 3040104659
---

---
## ELIGIBILITY 

1. All patients across all units

## VALIDITY for 1 hour epoch calculation (floorplan, individual chart & SPC)

1. If verbal pain scale = 2-4, verbal pain scale is only valid if within last 75 minutes  

2. If verbal pain scale = 0-1, verbal pain scale only valid if within last 4:15 (4 hours & 15 minutes) hours  

3. If verbal pain scale = ‘unable to assess’, verbal pain scale only valid if within last 4:15 hours

4. If CPOT = 3-8, CPOT scale only valid if within last 75 minutes 

5. If CPOT =  0-2, CPOT scale only valid if within last 4:15 hours

## CLASSIFICATION 

**[A] Pain Score Measurement Interval**
  
Feeds into (i) front tile - 24 hour rolling window and (ii) SPC interval charts.
  
**Front tile AVERAGE PAIN MEASUREMENT INTERVAL**
1. Measurement interval should be calculated from ACTUAL documented scores in EPIC and not any forward filled scores - these data have precise _dt stamps
2. There needs to be a minimum of two scores to calculate a measurement interval (if a patient only has one pain score during their ICU admission, this will not be included in the ‘average measurement interval’ data)
3. Any period of time where a patient is documented as off unit, e.g. for a scan or procedure, should not factor into the calculation. i.e. if pain assessment 1 of 2 in an interval has a dt_stamp directly before a time period when the patient is off the unit, this measurement and the interval between dt_stamp 1 and 2, which will occur after the patient has returned back to the unit should be excluded from the average. Time 2 of the interval when the patient returns should therefore become time 1 of the subsequent time interval. This is to avoid excessively long time intervals factoring into the average when there would not have been possible to document a pain score in the ICU notes. 
4. There are two different categories of measurement intervals that need to be calculated (refer to equivalence table VPS-CPOT):
   - a. GREEN measurement interval - no pain / mild pain or 'unable to assess'
   - b. AMBER/RED measurement interval - moderate / severe / very severe pain
5. When looking at the time interval between two measurements, look at the RAG label of the earlier _dt stamp and use this to allocate category (i.e. either green or red). This is required because when the pain measurement score changes for a patient between two measurements (e.g. it goes from mild to moderate) this will result in a measurement comparison between two different categories (i.e. green vs. red) but this is still a valid comparison for the purposes of this rule set. Note that this differs from measurement interval calculation used in RASS.
6. Pool (each categrory GREEN or AMBER/RED (i.e. not on an individial patient basis) measurement interval data for the 24 hour time period
7. Numerator = sum of time interval measurement (hours) 
8. Denominator (unadjusted) = number of time interval measurements
9. FRONT TILE AVERGAE MEASUREMENT INTERVAL (24 hour rolling window) - CALCLULATE MEAN using above numerator / denominator (unadjusted)
  
** SPC MEASUREMENT INTERVAL CHART (p-chart (%))**
  
9. Please see SPC pain score chart for denominator adjustment and calculation

**[B]  Create 1 hour epoch, RAG classification**
  
Feeds into (i) floor plan, (ii) individual patinet chart and (iii) SPC pain score charts.

1. Create label for each 1-hour epoch
2. There are four pain measurement possibilities: (1) VPS _move score, (2) VPS_rest score, (3) CPOT score and VPS 'unable to assess'
3. Pool all the pain measurements (VPS_move / VPS_rest / CPOT/ VPS 'unable to assess') for each individual patient into 1-hour epochs
4. Eliminate same _dt stamp:
5. If two or more measurements (of any type) have the same _dt stamp then retain the highest score for that time _dt stamp
6. If there is an equal highest score (with the same _dt stamp) accross two or more of VPS_move / VPS_rest / CPOT - then retain VPS_move over VPS_rest over CPOT
7. 1-hour epoch label (most recent score)
8. If there are two or more scores in a 1-hour epoch then take the most recent score, unless: (i) it is a CPOT score preceeded by a VPS_move/VPS_rest score, in which case retain the most recent VPS_move/VPS_rest score; or (ii) it is a VPS 'unable to assess' preceeded by a VPS_move/VPS_rest score/CPOT, in which case take the most recent VPS_move/VPS_rest score/CPOT
9. A 1-hour epoch should only carry a VPS ‘unable to assess’, if this is the only measuremnt in that hour, or it is preceeded by a VPS 'unable to assess'
10. If no valid score in the current 1-hour epoch, then forward fill, using above validity (time) rules (i.e. if green forward fill for 4:15 hours, if amber or red 75 minutes
11. NOTE - the VPS 'unable to assess' label will ONLY be used for the unit floorplan (where it will have its own specific label), it has no purpose in the individual patient pain score chart nor the SPC pain chart


   ## Table: equivalence between VPS & CPOT  
| Classification | VPS (rest/move) | CPOT | Transformed CPOT | Validity time | Colour |
|-|-|-|-|-|-|
| Unable to assess with 'other' filled | -1 |  |  | 4:15 hours | green |
| No | 0 | 0 | 0 | 4:15 hours | green |
| Mild | 1 | 1-2 | 1 | 4:15 hours | green |
| Moderate | 2 |  3-4 | 2 | 75 minutes | amber|
| Severe | 3 | 5-6 | 3| 75 minutes | red |
| Very severe | 4 | 7-8 | 4 | 75 minutes | red |

**[C] No pain / mild pain front tile calculation**
1. Front tile is a 24 hour rolling window (at each refresh looks back and collect all the pain scores for 24 hours)
2. Eliminate same _dt stamp: (a) if two or more measurements (of any type) have the same _dt stamp then retain the highest score for that time _dt stamp; (b) If there is an equal highest score (with the same _dt stamp) accross two or more of VPS_move / VPS_rest / CPOT - then retain VPS_move over VPS_rest over CPOT
3. Eliminate VPS 'unable to assess'
4. Use RAG classification to label each score
5. Numerator: All green scores (VPS_move 0 or 1; VPS_rest 0 or 1; CPOT 0, 1 or 2) in that 24 hour period
6. Denominator All scores in that 24 hour period
7. Calcualte and represent as a percentage for front tile 

**[D] Floorplan labelling**

1. If latest verbal pain scale reading = 0-1: ‘GREEN’; design = green filled bed 
2. If latest CPOT reading = 0-2: ‘GREEN’; design = green filled bed
3. If latest verbal pain scale reading = 2: ‘AMBER’; design = amber filled bed
4. If latest CPOT reading = 3-4: ‘AMBER’; design = amber filled bed
5. If latest verbal pain scale reading = 3-4: ‘RED’; design = red filled bed
6. If latest CPOT reading = 5-8: ‘RED’; design = red filled bed
7. If latest reading ‘missing’: ‘missing’; design = white filled bed with red hashed outline
8. If latest VPS reading is ‘unable to assess’, label as ‘unable to assess’. Design = white filled bed with blue hashed outline.

**[E] Epidural Floorplan labelling**

1. Label patient as 'on epidural' if there is a value equal or greater to zero in flowsheet 7001026 within the last 12 hours.
   
**[F] Classification Rules: Individual patient chart**

1. X-axis time in hours, range 0-72 hours, default to 24 hours
2. Y-axis left is pain score (VPS-0 to 4 and CPOT 0 to 8 adjusted to VPS equivalence (see label above)
3. DESIGN KEY FOR INDIVIDUAL CHARTS 
   - a. Label VPS as circles 
   - b. Label CPOT as diamonds
   - c. Colour code – RAG rated pain score (see equivalence table)
   - d. Missing – no data points
   - f. Forward filled data (see validity for 1 hour epoch calculation) shown as a continuing line (no icons circles/diamonds)
   - g. epidural- letter 'E' centred on bed

---
# [G] SPC CHARTS 

**PAIN SPC CHARTS (refer to 1-hour epoch, RAG classification [B]**

1. Calendar day defined as 00:00 - 23:59
2. Week defined as Monday 00:00 – Sunday 23:59


## Chart 1 [Patient chart] 
**Proportion of moderate or severe pain scores – weekly chart**

Operational definition = of the documented pain scores in EPIC, what proportion are moderate or severe on a weekly basis? 

1. Look at 1-hour epoch RAG classification
2. Exclude 1-hour epochs that have a VPS 'unable to assess' label
3. Exclude all 1-hour epochs that have been back filled
4. You should now only have 1-hour epochs that were generated using an actual measurement (has a _dt stamp) of VPS _move/VPS_rest/CPOT score
5. Numerator = For each individual patient: count the number of AMBER/RED 1-hour epochs in one calendar day (day_numerator)
6. Denominator = Count all the 1-hour epochs in that calendar day that were generated by an actual measurement (day-denominator)
7. Calculate the day percentage of AMBER/RED 1-hour epochs: day_numerator / day_denominator for each patient on each calendar day in the designated week
8. SPC data point = calculate aggregated mean of all the patient_day percentages during the designated week - plot on p-chart SPC
   
*note rationale for use of calendar day: reduces confounder for variation in pain due to type of operation*
    

### n-number for process limit calculation

Number of patients present on the unit in the calendar week. 

*note we may want to come back to this and replace with n number which is the sample size of measurements, rather than patients (aggregated sum of point 6 above). 

Tooltip display = process limit n-number with the label "eligible patients".

  
   
**INTERVAL SPC CHARTS (refer to derived data from 'Pain Score Assessment Measurement Interval [A])**
1. These are weekly percentage (p-charts) SPC
2. Week defined a Monday 00:00 – Sunday 23:59

## Chart 2a GREEN [Assessment Measurement Interval Chart] - none to mild pain 
1. Look at GREEN category measurement intervals in that week
2. Numerator = count of time intervals that are ≤ 4:00 hours for the GREEN category
3. Denominator = count of all GREEN category time intervals (unadjusted)
4. SPC denominator adjustment required for excessively long measurement intervals (those that are 2x accepted measurement interval from clinical guidance)
5. Denominator (adjusted) = count all measurement intervals in the GREEN category in that week that are >8:00 hours and ADD +1 to denominator for each four hour period greater than the permitted 4:00 hours
6. For example: (i) an 8:01hr (8:01-12:00) measurement interval will count as 2 in the adjusted denominator - once for the measurement and once for being an additional 4:00hr over the permitted four hours for this category; (ii) 12:01hr (12:01-16:00) measurement interval will count as 3 in the adjusted denominator; (iii) 16:01hr (16:01-20:00) measurement interval will count as 4 in the adjusted denominator etc...
7. Generate percentage of measurement intervals for that week that are 4:00 hours or less: numerator / denominator (adjusted)
8. Plot on weekly chart

 ### n number for process limit calculation

Point 3 above- count of all GREEN category time intervals (unadjusted)

Tooltip display = process limit n-number with the label "number of measurements".

## Chart 2b AMBER/RED [Assessment Measurement chart] - moderate severe pain 
1. Look at AMBER/RED category measurement intervals in that week
2. Numerator = count of time intervals that are ≤ 1:00 hour for the AMBER/RED category
3. Denominator = count of all AMBER/RED category time intervals (unadjusted)
4. SPC denominator adjustment required for excessively long measurement intervals (those that are 2x accepted measurement interval from clinical guideance)
5. Denominator (adjusted) = count all measurement intervals in the AMBER/RED category in that week that are >1:00 hours and ADD +1 to denominator for each one hour period greater than the permitted 1:00 hours
6. For example: (i) an 2:01hr (2:01-3:00) measurement interval will count as 2 in the adjusted denominator - once for the measurement and once for being an additional 1:00hr over the permitted four hours for this category; (ii) 3:01hr (3:01-4:00) measurement interval will count as 3 in the adjusted denominator; (iii) 4:01hr (4:01-5:00) measurement interval will count as 4 in the adjusted denominator etc...
7. Generate percentage of measurement intervals for that week that are 1:00 hour or less: numerator / denominator (adjusted)
8. Plot on weekly chart


 ### n number for process limit calculation

Point 3 above- count of all AMBER/RED category time intervals (unadjusted)

Tooltip display = process limit n-number with the label "number of measurements".
