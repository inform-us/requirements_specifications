# Pain rules
Some description here...

## EPIC
- There will only be two pain scores going forward
  - Verbal pain score
  - Critical Care Pain Observation Tool (CPOT) - scale 0-8
- Pain scale value is an integer (EPIC will allow free text!)
- There are no targets for these variables

## EPIC Flowsheets
* ### Verbal Pain Scale (VPS)
 - Verbal Pain Scale (at rest) - Row ID 3040104280
 - Verbal Pain Scale (at movement) - Row ID 3040104281

* ### Critical Care Observation Tool (CPOT) - components
- Facial Expression    -                           			Row ID 3040104654
- Body Movements       -                        		   	Row ID 3040104655 
- Compliance with Ventilator     -                			Row ID 3040104656

Or

- Vocalization (Extubated patients)  -  			Row ID 3040104657
- Muscle Tension                      -                			Row ID 3040104658
- CRITICAL CARE PAIN OBSERVATION SCORE  -  Row ID 3040104659
---

## ELIGIBILITY 

1. All patients across all units

## VALIDITY (time window)

1. If verbal pain scale = 2-4, verbal pain scale is only valid if within last 75 minutes  

2. If verbal pain scale = 0-1, verbal pain scale only valid if within last 5 hours  

3. If verbal pain scale = ‘unable to assess’ valid for 5 hours 

4. If CPOT = 3-8 CPOT scale only valid if within last 75 minutes 

5. If CPOT =  0-2 CPOT scale only valid if within last 5 hours

## CLASSIFICATION 

**[A] Pain scales Measurement interval** 

1. Measurement interval should be calculated from actual documented scores in EPIC and not any forward filled scores. These data have precise d/t stamps.
2. There are two different measurement intervals that need to be calculated 
   - a. Measurement interval for GREEN (none/mild pain or unable to assess) 
   - b. Measurement interval for AMBER/RED (moderate/severe/very severe pain)
3. When looking at the time interval between two measurements, look at the RAG label for the earlier _dt stamp and use this to allocate category (this differs from measurement interval calculation used in RASS)
4. The mean measurement interval in the preceding 24 hours is then calculated for each respective measurement interval (GREEN & AMBER/RED)
5. There needs to be a minimum of two scores to calculate a measurement interval. If a patient only has one pain score during their ICU admission, this will not/cannot be included in the ‘average measurement interval’ data.

**[B]  Create 1 hour epoch, RAG classification**

1. Create label for each 1-hour epoch
2. If both CPOT and VPS score are documented, use highest score for that 1 hour epoch.
3. If both CPOT and VPS scores are documented AND are equal, use VPS score.
4. If both valid VPS at rest and at movement recorded, then use highest value score for that 1 hour epoch
5. If both VPS at movement and rest scores are documented AND are equal, then use ‘at movement’ score
6. If two of the same type of scores are documented (e.g. two VPS as rest in one epoch), use most recent score
7. If both VPS ‘unable to assess’ AND CPOT are entered, use CPOT score
8. If no valid score in the current epoch, then forward fill, using above validity (time) rules (i.e. if green forward fill for 5 hours, if amber or red 75 minutes.


   ## Table: equivalence between VPS & CPOT  
| Classification | VPS (rest/move) | CPOT | Transformed CPOT | Validity time | Colour |
|-|-|-|-|-|-|
| Unable to assess with 'other' filled | 0 |  |  | 5 hours | green |
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


