## List of all existing and upcoming inform_us metrics and their corresponding flowsheet IDs in EPIC ##

James ran some EMAP queries for all of the below flowsheet ID's on 24.05.2024. I added a final column to the table to indicate what the results of the queries were. ❌ indicates that no data at all was returned, while ✅ indicates that I successfully got data back for patients that were currently on the unit.


| Tile | Metric | Flowsheet ID | data available in EMAP? |
|-|-|-|-|
| CAM -ICU | Feature 1: Acute Onset or Fluctuating Course | 3040104645 | ❌ |
| CAM -ICU | Feature 2: Inattention | 3040104647 | ❌ |
| CAM -ICU | Feature 3: Altered Level of Consciousness | 3040104648 | ❌ |
| CAM-ICU | Feature 4: Disorganized Thinking | 3040104649 | ❌ |
| CAM-ICU | Overall CAM-ICU | 3040104650 | ✅ | 
| | | |
| Epidural | Level of Block (Left side) | 38580 | ❌ |
| Epidural | Level of Block (Right side) | 38581 | ❌ |
| Epidrual | Assessment of Motor Block Lt leg | 30415249 | ❌ |
| Epidural | Assessment of Motor Block Rt leg | 30415250 | ❌ |
| Epidural | Epidural catheter | 7080610 | ❌ |
| | | |
| Epidural drugs | Bupivacane 0.1% Epidural infusion prescription | 191107 | ❌ |
| Epidural drugs | Bupivacane 0.1% with fentanyl 2mcg/ml epidural infusion prescription | 30863 | ❌ |
| Epidural drugs | Bupivacaine 0.1% with fentanyl 2mcg/ml PIEB epidural infusion | 40830864 | ❌ |
| Epidural drugs | Bupivacaine 0.1% with fentanyl 2mcg/ml PCEA epidural infusion (EGA) | 40830863 | ❌ |
| Epidural drugs | Bupivacane 0.1% with fentanyl 2mcg/ml epidural injection (EGA only) 20mls | 408124007 | ❌ |
| Epidural drugs | Levobupivacaine 0.1% with fentanyl 2 mcg/ml epidural infusion | 188047 | ❌ |
| Epidural drugs | Levobupivacaine 0.1% with fentanyl 2 mcg/ml  PCEA epidural infusion | 408133001 | ❌ |
| Epidural drugs | Levobupivacaine 0.125% epidural infusion 100ml | 181761 | ❌ |
| Epidural drugs | Levobupivacaine 0.125% epidural infusion 200ml | 181762 | ❌ |
| Epidural drugs | PCEA theatres bupivacaine 0.1% epidural infusion (aka EPIDURAL) | 408107895 | ❌ |
| Epidural drugs | PCEA theatres bupivacaine 0.1% with fentanyl 2mcg/ml epidural infusion (aka EPIDURAL) | 408107894 | ❌ |
| | | |
| Airway | ETT| 400655 | ❌ |
| Airway | Surgical Airway | 7070173 | ❌ |
| Airway | Supraglottic Airway | 1120100089 | ❌ |
| Airway | Airway plan | 23864 | ❌ |
| | | | 
| PACU | Ready for discharge | 41222 | ✅ |
| PACU | Post op surgical | 1169 | ❌ |
| PACU | Fluid intake | 42532 | ❌ |
| PACU | Oral Fluids Offered | 6374 | ❌ |
| PACU | Fluid intake | 45429 | ❌ |
| PACU | Nutritional intake | 42701 | ❌ |
| PACU | Food offered | 6375 | ❌ |
| PACU | Diet Intake | 6482 | ❌ |
| PACU | Amount Eaten | 6484 | ❌ |
| PACU | Mobilisation | 42700 | ❌ |
| PACU | Mobilisation achieved by patient | 40705 | ❌ |
| PACU | Distance walked | 42533 | ❌ | 
| PACU | Step count | 44741 | ❌ |
| | | |

## Trimmed down list of minimum Flowsheet IDs needed for next metrics on dashboard##

| Tile | Metric | Flowsheet ID | data available in EMAP? | Expected frequency of documentation (according to guideline)
|-|-|-|-|
| CAM-ICU | Overall CAM-ICU | 3040104650 | ✅ | Documented once per 12-hour shift (once between 0800-1959 and once between 2000-0759)|
| | | |
| Epidural | Level of Block (Left side) | 38580 | ❌ | Documented two hourly 0800-2000 and four hourly 2001-0759 |
| Epidural | Level of Block (Right side) | 38581 | ❌ | Documented two hourly 0800-2000 and four hourly 2001-0759 |
| Epidrual | Assessment of Motor Block Lt leg | 30415249 | ❌ | Documented two hourly 0800-2000 and four hourly 2001-0759 |
| Epidural | Assessment of Motor Block Rt leg | 30415250 | ❌ | Documented two hourly 0800-2000 and four hourly 2001-0759 |
| Epidural | Epidural catheter | 7080610 | ❌ |
| | | |
| Epidural drugs | Bupivacane 0.1% Epidural infusion prescription | 191107 | ❌ | Real time |
| Epidural drugs | Bupivacane 0.1% with fentanyl 2mcg/ml epidural infusion prescription | 30863 | ❌ | Real time |
| Epidural drugs | Bupivacaine 0.1% with fentanyl 2mcg/ml PIEB epidural infusion | 40830864 | ❌ | Real time |
| Epidural drugs | Bupivacaine 0.1% with fentanyl 2mcg/ml PCEA epidural infusion (EGA) | 40830863 | ❌ | Real time |
| Epidural drugs | Bupivacane 0.1% with fentanyl 2mcg/ml epidural injection (EGA only) 20mls | 408124007 | ❌ | Real time |
| Epidural drugs | Levobupivacaine 0.1% with fentanyl 2 mcg/ml epidural infusion | 188047 | ❌ |  Real time |
| Epidural drugs | Levobupivacaine 0.1% with fentanyl 2 mcg/ml  PCEA epidural infusion | 408133001 | ❌ |  Real time |
| Epidural drugs | Levobupivacaine 0.125% epidural infusion 100ml | 181761 | ❌ |  Real time |
| Epidural drugs | Levobupivacaine 0.125% epidural infusion 200ml | 181762 | ❌ |  Real time |
| Epidural drugs | PCEA theatres bupivacaine 0.1% epidural infusion (aka EPIDURAL) | 408107895 | ❌ |  Real time |
| Epidural drugs | PCEA theatres bupivacaine 0.1% with fentanyl 2mcg/ml epidural infusion (aka EPIDURAL) | 408107894 | ❌ |  Real time |
| | | |
| Airway | ETT| 400655 | ❌ |
| Airway | Surgical Airway | 7070173 | ❌ |
| Airway | Supraglottic Airway | 1120100089 | ❌ |
| Airway | Airway plan | 23864 | ❌ |
| | | | 
| PACU | Ready for discharge | 41222 | ✅ |
| PACU | Post op surgical | 1169 | ❌ |
| PACU | Fluid intake | 42532 | ❌ |
| PACU | Oral Fluids Offered | 6374 | ❌ |
| PACU | Fluid intake | 45429 | ❌ |
| PACU | Nutritional intake | 42701 | ❌ |
| PACU | Food offered | 6375 | ❌ |
| PACU | Diet Intake | 6482 | ❌ |
| PACU | Amount Eaten | 6484 | ❌ |
| PACU | Mobilisation | 42700 | ❌ |
| PACU | Mobilisation achieved by patient | 40705 | ❌ |
| PACU | Distance walked | 42533 | ❌ | 
| PACU | Step count | 44741 | ❌ |
| | | |
