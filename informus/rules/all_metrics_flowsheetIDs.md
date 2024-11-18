# List of all existing and upcoming inform_us metrics and their corresponding flowsheet IDs in EPIC ##

Query ran: 2024/06/10

- `has_visit_observation` ✅ indicates that data is available in EPIC and is pulled through to EMAP `star`. Items with ✅ in this column but not in `is_real_time` can be added to the HL7 feed to provide real-time data.
- `is_real_time` ✅ shows whether real-time data is available in EMAP. Once the flowsheet is activated in `star` we can ask the EMAP team to activate `is_real_time` for that flowsheet.
- An ❌ in `has_visit_observation` means we cannot request this flowsheet to be activated in EMAP. So we will have to explore `caboodle` to see if there are any alternative flowsheets that we might be able to use.

| Tile | Metric | Flowsheet ID | `star.has_visit_observation` is `True` | `star.is_real_time` is `True`  | frequency of reporting | Found in `star.visit_observation_type` | EPIC ID | Status |
|-|-|-|-|-|-|-|-|-|
| CAM-ICU | Overall CAM-ICU | 3040104650 | ✅ | ✅ | Once between 0800-1959 and once between 2000-0759 | ✅ | ? | complete (flowsheet is in EMAP) |
| | | | | | | | | |
| Epidural | Level of Block (Left side) | 38580 | ✅ | ✅ | 2-hourly between 0800-1959, 4-hourly between 2000-0759 | ✅ | ? | complete (flowsheet is in EMAP) |
| Epidural | Level of Block (Right side) | 38581 | ✅ | ✅ | 2-hourly between 0800-1959, 4-hourly between 2000-0759 | ✅ | ? | complete (flowsheet is in EMAP) |
| Epidrual | Assessment of Motor Block Lt leg | 30415249 | ✅ | ✅ | 2-hourly between 0800-1959, 4-hourly between 2000-0759 | ✅ | ? | complete (flowsheet is in EMAP) |
| Epidural | Assessment of Motor Block Rt leg | 30415250 | ✅ | ✅ | 2-hourly between 0800-1959, 4-hourly between 2000-0759 | ✅ | ? | complete (flowsheet is in EMAP) |
| Epidural | LDA line status simple | 3040102506 | ✅ | ✅ |  | ✅ | ? | complete (flowsheet is in EMAP) |
| | | | | | | | | |
| Epidural drugs | PCEA theatres bupivicaine 0.1% with fentanyl 2mcg/ml epidural infusion | 28222 | ❌ | ❌ |  | ❌ | 408107894 | p |
| Epidural drugs | bupivicaine 0.1% epidural infusion | 7001026 | ❌ | ❌ | hourly | ❌ | 191107 | p |
| Epidural drugs | bupivicaine 0.1% with fentanyl 2mcg/ml epidural infusion | ? | ❌ | ❌ | hourly | ❌ | 30863 | p |
| Epidural drugs | bupivicaine 0.1% with fentanyl 2mcg/ml PIEB epidural infusion | 31429 | ❌ | ❌ | hourly | ❌ | 40830864 | p |
| Epidural drugs | bupivicaine 0.1% with fentanyl 2mcg/ml PCEA epidural infusion | ? | ❌ | ❌ | hourly | ❌ | 40830863 | p |
| Epidural drugs | Bupivacane 0.1% with fentanyl 2mcg/ml epidural injection (EGA only) 20mls | ? | ❌ | ❌ | hourly | ❌ | 408124007 | p |
| Epidural drugs | levobupivicaine 0.125% wtih fentanyl  2mch/ml epidural infusion | ? | ❌ | ❌ | hourly | ❌ | 188047 | p |
| Epidural drugs | Levobupivacaine 0.1% with fentanyl 2 mcg/ml  PCEA epidural infusion | 48330 | ❌ | ❌ | hourly | ❌ | 408133001 | p |
| Epidural drugs | levobupivicaine 0.125% epidural infusion (100ml) | 7001026 | ❌ | ❌ | hourly | ❌ | 181761 | p |
| Epidural drugs | levobupivicaine 0.125% epidural infusion (200ml) | ? | ❌ | ❌ | hourly | ❌ | 181762 | p |
| Epidural drugs | PCEA theatres bupivicaine 0.1% epidural infusion | ? | ❌ | ❌ | hourly | ❌ | 408107895 | p |
| Epidural drugs | R UCLH PIEB BUPIVACAINE (0.125%) / FENTANYL (2 MCG/ML) - VOLUME INFUSED, Volume Infused (mL) Bupivacaine (0.125%) / Fentanyl (2 mcg/mL) | 47779 (Harry said there is no data avilable for this, so we can't use it) | ❌ | ❌ | hourly | ❌ | ? | p |
| Epidural drugs | R UCLH PCEA BUPIVACAINE (0.125%) / FENTANYL (2 MCG/ML) - CUMULATIVE INTAKE, Volume Infused (mL) Bupivacaine (0.125%)/Fentanyl (2 mcg /mL) | 47756 | ❌ | ❌ |  | ❌ | ? | p |
| | | | | | | | | |
| Airway | Airway plan | 24499 | ✅ | ✅ | once per admission | ✅ | ? | complete (flowsheet is in EMAP) |
| Airway | Airway plan A | 23865 | ✅ | ✅ |  | ✅ | ? | complete (flowsheet is in EMAP) |
| Airway | Airway plan B | 23866 | ✅ | ✅ |  | ✅ | ? | complete (flowsheet is in EMAP) |
| Airway | Airway plan C | 23867 | ✅ | ✅ |  | ✅ | ? | complete (flowsheet is in EMAP) |
| Airway | 02 delivery method | 3040109305 | ✅ | ✅ |  | ✅ | ? | complete (flowsheet is in EMAP) |
| Airway| Intubation grade| 37950 | ✅ | ✅ | | ✅ | ? | complete (flowsheet is in EMAP) |
| Airway| Has Generic Airway Plan| 24498 | ✅ | ✅ | | ✅ | ? | complete (flowsheet is in EMAP) |
| | | | | | | | | |
| DrEaMing | Fluid intake | 45429 | ✅ | ✅ | real-time | ✅ | ? | complete (flowsheet is in EMAP) |
| DrEaMing | Diet Intake - *type of diet patient is on* | 6482 | ✅ | ✅ | real-time | ✅ | ? | complete (flowsheet is in EMAP) |
| DrEaMing | Mobilisation achieved by patient - *scale of mobilising from none to walking independently* | 40705 | ✅ | ✅ | real-time | ✅ | ? | complete (flowsheet is in EMAP) |
| DrEaMing | Mobility scale reasons | 47371 | ✅ | ✅ | real-time | ✅ | ? | complete (flowsheet is in EMAP) |
| | | | | | | | | |
