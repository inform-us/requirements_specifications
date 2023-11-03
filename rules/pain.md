# Pain rules
Some description here...

## EPIC
- There will only be two pain scores (in EPIC) going forward
  - Verbal pain score - scale 0-4
  - Critical Care Pain Observation Tool (CPOT) - scale 0-8
- Pain scale value is an integer (EPIC will allow free text!)
- There are no targets for these variables

## EPIC Flowsheets
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

## VALIDITY for 1 hour epoch calculation (time window)

1. If verbal pain scale = 2-4, verbal pain scale is only valid if within last 75 minutes  

2. If verbal pain scale = 0-1, verbal pain scale only valid if within last 5 hours  

3. If verbal pain scale = ‘unable to assess’, verbal pain scale only valid if within last 5 hours

4. If CPOT = 3-8, CPOT scale only valid if within last 75 minutes 

5. If CPOT =  0-2, CPOT scale only valid if within last 5 hours

## CLASSIFICATION 

**[A] Pain Score Measurement Interval**
  
Feeds into (i) front tile - 24 hour rolling window and (ii) SPC interval charts.
1. Measurement interval should be calculated from ACTUAL documented scores in EPIC and not any forward filled scores - these data have precise _dt stamps
2. There needs to be a minimum of two scores to calculate a measurement interval (if a patient only has one pain score during their ICU admission, this will not be included in the ‘average measurement interval’ data)
3. There are two different categories of measurement intervals that need to be calculated (refer to equivalence table VPS-CPOT):
   - a. GREEN measurement interval - no pain / mild pain or 'unable to assess'
   - b. AMBER/RED measurement interval - moderate / severe / very severe pain
4. When looking at the time interval between two measurements, look at the RAG label for the earlier _dt stamp and use this to allocate category (this differs from measurement interval calculation used in RASS)
5. Pool (not individial patient basis) measurement interval data for the 24 hour time period
6. Numerator = number of measurements
7. Denominator (unadjusted) = number of measurements
8. Denominator adjustment required for excessively long measurememnt intervals (those that are 2x accepted measurement interval from clincal guideance)
9. GREEN category: count the number of measurement intervals that are >8:00hr in the 24 hour period and add +1 to denominator for each four hour period greater than the permitted 4:00hr
10. For example: (i) an 8:01hr measurement interval will count as 2 in the adjusted denominator - once for the measurement and once for being an additional 4:00hr over the permitted four hours for this category; (ii) 12:01hr measurement interval will count as 3 in the adjusted denominator; (iii) 16:01hr measurement interval will count as 4 in the adjusted denominator etc...
11. AMBER/RED category: count the number of measurement intervals that are >2:00hr in the 24 hour period and add +1 to denominator for each one hour eperiod greater than the permitted 1:00hr
12. For example: (i) an 2:01hr measurement interval will count as 2 in the adjusted denominator - once for the measurement and once for being an additional 1:00hr over the permitted four hours for this category; (ii) 3:01hr measurement interval will count as 3 in the adjusted denominator; (iii) 4:01hr measurement interval will count as 4 in the adjusted denominator etc...
13. Calculate the (adjusted) mean measurement interval in the preceding 24 hours for each respective measurement interval category (GREEN & AMBER/RED) using the NUMERATOR / adjusted DENOMINATOR

**[B]  Create 1 hour epoch, RAG classification**
  
Feeds into (i) floor plan, (ii) individual patinet chart and (iii) SPC pain score charts.

1. Create label for each 1-hour epoch
2. There are four pain measurement possibilities: (1) VPS _move score, (2) VPS_rest score, (3) CPOT score and VPS 'unable to assess'
3. Pool all the pain measurements (VPS_move / VPS_rest / CPOT/ VPS 'unable to assess') for each individual patient into 1-hour epochs
4. Eliminate same _dt stamp:
5. If two or more measurements (of any type) have the same _dt stamp then retain the highest score for that time _dt stamp
6. If there is an equal highest score (with the same _dt stamp) accross two or more of VPS_move / VPS_rest / CPOT - then retain VPS_move over VPS_rest over CPOT
7. 1-hour epoch label (most recent score):
8. If there are two or more scores in a 1-hour epoch then take the most recent score, unless: (i) it is a CPOT score preceeded by a VPS_move/VPS_rest score, in which case retain the most recent VPS_move/VPS_rest score; or (ii) it is a VPS 'unable to assess' preceeded by a VPS_move/VPS_rest score/CPOT, in which case take the most recent VPS_move/VPS_rest score/CPOT
9. A 1-hour epoch should only carry a VPS ‘unable to assess’, if this is the only measuremnt in that hour, or it is preceeded by a VPS 'unable to assess'
10. If no valid score in the current 1-hour epoch, then forward fill, using above validity (time) rules (i.e. if green forward fill for 5 hours, if amber or red 75 minutes
11. NOTE - the VPS 'unable to assess' label will ONLY be used for the unit floorplan (where it will have its own specific label), it has no purpose in the individual patient pain score chart nor the SPC pain chart


   ## Table: equivalence between VPS & CPOT  
| Classification | VPS (rest/move) | CPOT | Transformed CPOT | Validity time | Colour |
|-|-|-|-|-|-|
| Unable to assess with 'other' filled | -1 |  |  | 5 hours | green |
| No | 0 | 0 | 0 | 5 hours | green |
| Mild | 1 | 1-2 | 1 | 5 hours | green |
| Moderate | 2 |  3-4 | 2 | 75 minutes | amber|
| Severe | 3 | 5-6 | 3| 75 minutes | red |
| Very severe | 4 | 7-8 | 4 | 75 minutes | red |



**[C] Floorplan labelling**

1. If latest verbal pain scale reading = 0-1: ‘GREEN’; design = green filled bed 
2. If latest CPOT reading = 0-2: ‘GREEN’; design = green filled bed
3. If latest verbal pain scale reading = 2: ‘AMBER’; design = amber filled bed
4. If latest CPOT reading = 3-4: ‘AMBER’; design = amber filled bed
5. If latest verbal pain scale reading = 3-4: ‘RED’; design = red filled bed
6. If latest CPOT reading = 5-8: ‘RED’; design = red filled bed
7. If latest reading ‘missing’: ‘missing’; design = white filled bed with blue hashed outline
8. If latest VPS reading is ‘unable to assess’, label as ‘unable to assess’. Design = white filled bed with green hashed outline.


**[D] Classification Rules (corresponds to pain per patient chart)

1. X-axis time in hours (range 24-72 hours)
2. Y-axis left is VPS (0-4) & Y-axis right is CPOT (0-8)
3. DESIGN KEY FOR INDIVIDUAL CHARTS 
   - a. Label VPS as circles 
   - b. Label CPOT as diamonds
   - c. Colour code – RAG rated pain severity
   - d. Non-numerical – hashed / dotted outline
   - e. Missing – no data points
   - f.‘Unable to assess’ - white circle with green hashed outline. 

---
# SPC CHARTS 
## Chart 1 [Patient chart] 
**Proportion of time in moderate or severe pain – weekly chart**
- Take individual patient label / reading for each 1 hour epoch 
- Count number of amber / red (A/R) hours  
- Divide by total number of eligible hours (hours with a valid pain score) for that patient in that calendar day period (accounts for missing bias)  
- Number of hours A/R / Total hours (for that patient)  
- Convert into percentage of hours spent in A/R (for each patient)  
- Pool every patient percentage (individual patient day) into a weekly aggregate (all patients)  
- Generate a weekly mean value (weekly aggregation) 
- Week defined a Monday 00:00 – Sunday 23:59

## Chart 2a GREEN [Interval chart] none to mild pain 
**Measurement interval – weekly chart**
- Week defined a Monday 00:00 – Sunday 23:59 
- Look at GREEN measurement category in a week 
- Numerator = count measurement intervals that are ≤ 4:00 hours 
- Denominator = count all measurement intervals in the GREEN category in that week 
- Generate percentage of measurement intervals that are 4:00 hours or less 
- Plot on weekly chart

## Chart 2b AMBER/RED [Interval chart] moderate severe pain 
**Measurement interval – weekly chart** 
- Week defined a Monday 00:00 – Sunday 23:59 
- Look at AMBER/RED measurement category in a week 
- Numerator = count measurement intervals that are ≤ 1:00 hour 
- Denominator = count all measurement intervals in the AMBER/RED category in that week 
- Generate percentage of measurement intervals that are 1:00 hour or less 
- Plot on weekly chart

  Anotation: We acknowledge the possibility of VPS at rest being a higher reading than VPS at movement though this is unlikely and therefore in the event that both scores are documented we select VPS at movement. 
  Questions for clarification : Is the prioritisation of pain scores the same for SPC as for the RAG classification? If yes, is that written in this part of the code?
  Are we happy with the decision to exclude CPOT when entered at the same time than VPS ( though it might not be the exact same time stamp)?


