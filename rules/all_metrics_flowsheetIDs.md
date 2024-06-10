# List of all existing and upcoming inform_us metrics and their corresponding flowsheet IDs in EPIC ##

James ran some EMAP queries for all of the below flowsheet ID's on 24.05.2024. I added a final column to the table to indicate what the results of the queries were. ❌ indicates that no data at all was returned, while ✅ indicates that I successfully got data back for patients that were currently on the unit.

| Tile | Metric | Flowsheet ID | `has_visit_observation` is `True` | `is_real_time` is `True`  |frequency of reporting | Found in `star.visit_observation_type` |
|-|-|-|-|-|-|-|
| CAM-ICU | Overall CAM-ICU | 3040104650 | ✅ | ❌ | Once between 0800-1959 and once between 2000-0759 | ✅ |
| | | | | | | |
| Epidural | Level of Block (Left side) | 38580 | ✅ | ✅ | 2-hourly between 0800-1959, 4-hourly between 2000-0759 | ✅ |
| Epidural | Level of Block (Right side) | 38581 | ✅ | ✅ | 2-hourly between 0800-1959, 4-hourly between 2000-0759 | ✅ |
| Epidrual | Assessment of Motor Block Lt leg | 30415249 | ✅ | ✅ | 2-hourly between 0800-1959, 4-hourly between 2000-0759 | ✅ |
| Epidural | Assessment of Motor Block Rt leg | 30415250 | ✅ | ✅ | 2-hourly between 0800-1959, 4-hourly between 2000-0759 | ✅ |
| Epidural | Epidural catheter | 7080610 | ❌ | ❌ |  note this is on avatar | ✅ |
| | | | | | | |
| Epidural drugs | Bupivacane 0.1% Epidural infusion prescription | 191107 | ❌ | ❌ | hourly | ❌ |
| Epidural drugs | Bupivacane 0.1% with fentanyl 2mcg/ml epidural infusion prescription | 30863 | ❌ | ❌ | hourly | ❌ |
| Epidural drugs | Bupivacaine 0.1% with fentanyl 2mcg/ml PIEB epidural infusion | 40830864 | ❌ | ❌ | hourly | ❌ |
| Epidural drugs | Bupivacaine 0.1% with fentanyl 2mcg/ml PCEA epidural infusion (EGA) | 40830863 | ❌ | ❌ | hourly | ❌ |
| Epidural drugs | Bupivacane 0.1% with fentanyl 2mcg/ml epidural injection (EGA only) 20mls | 408124007 | ❌ | ❌ | hourly | ❌ |
| Epidural drugs | Levobupivacaine 0.1% with fentanyl 2 mcg/ml epidural infusion | 188047 | ❌ | ❌ | hourly | ❌ |
| Epidural drugs | Levobupivacaine 0.1% with fentanyl 2 mcg/ml  PCEA epidural infusion | 408133001 | ❌ | ❌ | hourly | ❌ |
| Epidural drugs | Levobupivacaine 0.125% epidural infusion 100ml | 181761 | ❌ | ❌ | hourly | ❌ |
| Epidural drugs | Levobupivacaine 0.125% epidural infusion 200ml | 181762 | ❌ | ❌ | hourly | ❌ |
| Epidural drugs | PCEA theatres bupivacaine 0.1% epidural infusion (aka EPIDURAL) | 408107895 | ❌ | ❌ | hourly | ❌ |
| Epidural drugs | PCEA theatres bupivacaine 0.1% with fentanyl 2mcg/ml epidural infusion (aka EPIDURAL) | 408107894 | ❌ | ❌ | hourly | ❌ |
| | | | | | | |
| Airway | Airway plan| 24499 | ✅ | ✅ | once per admission | ✅ |
| Airway| Intubation grade| 37950 | ✅ | ✅ | | ✅ |
| Airway| Das Generic Airway Plan| 24498 | ✅ | ✅ | | ✅ |
| Airway | ETT-*on avatar* | 400655 | ❌ | ❌ | | ✅ |
| Airway | Surgical Airway- *surgical trache* | 7070173 | ❌ | ❌ | once | ✅ |
| Airway | Supraglottic Airway- *trache* | 1120100089 | ❌ | ❌ |  once  | ✅ |
| Airway | Non-surgical Airway - *trache placed without surgery* | 400638 | ❌ | ❌ | once | ✅ |
| | | | | | | |
| PACU | Ready for discharge | 41222 | ✅ | ✅ | real-time | ✅ |
| PACU | Fluid intake | 45429 | ❌ | ❌ | real-time | ✅ |
| PACU | Diet Intake - *type of diet patient is on* | 6482 | ❌ | ❌ | real-time | ✅ |
| PACU | Amount Eaten | 6484 | ❌ | ❌ | real-time | ✅ |
| PACU | Mobilisation achieved by patient - *scale of mobilising from none to walking independently* | 40705 | ❌ | ❌ | real-time | ✅ |
| | | | | | | |
