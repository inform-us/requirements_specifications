SPC chart status of latest changes -June 2025


SPC Chart n-number denominators


| Table name                  | Denominator label | Details                                                                                                                                         |
|----------------------------|-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
| spc_airway                 | eligible_patients | the number of patients who have been present on each unit in the week.                                                                          |
| spc_all_targets            | eligible_patients |  aggregated (weekly) denominator: total number of current patients (occupied beds) at 13:30 hours                                               |
| spc_pain_rag_amber_red     | eligible_patients | Number of patients present on the unit in the calendar week.                                                                                     |
| spc_o2_inrange             | eligible_patients | total of patients that contributed to the in range reading (not NaN or zero in the in_range_pct column)                                         |
| spc_o2_above               | eligible_patients | total of patients that contributed to the above reading (not NaN or zero in the above_pct column)                                               |
| spc_o2_below               | eligible_patients | total_below_patients                                                                                                                             |
| spc_map_inrange            | eligible_patients | total of patients that contributed to the in range reading (not NaN or zero in the in_range_pct column)                                         |
| spc_map_above              | eligible_patients | total of patients that contributed to the above reading (not NaN or zero in the above_pct column)                                               |
| spc_map_below              | eligible_patients | total_below_patients                                                                                                                             |
| spc_tidal_volume_on_target | eligible_patients | Total patients that contributed to the target percentage reading - including percentage that is zero (as zero percentage means denominator ≠ 0) |
| spc_rass_on_target         | eligible_patients | Total patients that contributed to the target percentage reading - including percentage that is zero (as zero percentage means denominator ≠ 0) |
| spc_delirium_calendar_day     | days_with_label   | number of patients present on each calendar day                                                                                              |
| spc_delirium_day_shift        | days_with_label   | number of patients present on each day shift                                                                                                 |
| spc_delirium_documentation    | days_with_label   | all patients present each shift with at least one a RASS score of -3 to +4 documented during that shift                                     |
| spc_delirium_night_shift      | days_with_label   | number of patients present on each night shift                                                                                               |
| spc_epidural_interval_four_hrs| days_with_label   | the average of number of measurement for left and right motor block that been taken at night                                                |
| spc_epidural_interval_two_hrs | days_with_label   | the average of number of measurement for left and right motor block that been taken at day                                                  |
| spc_pain_interval_four_hrs    | days_with_label   | count of all AMBER/RED category time intervals (unadjusted)                                                                                 |
| spc_pain_interval_one_hrs     | days_with_label   | count of all GREEN category time intervals (unadjusted)                                                                                      |
| spc_rass_interval_four_hrs    | days_with_label   | count of all night category time intervals (unadjusted)                                                                                      |
| spc_rass_interval_one_hrs     | days_with_label   | count of all day category time intervals (unadjusted)                                                                                        |
| spc_dreaming                  | days_with_label   | aggregated (weekly) denominator: total number of patients (including discharged and RIP) present on unit (based on CSNs) between 00:00–23:59 |


| SPC Chart | Recalc formula up to date i.e. 12 | Denominator up to date? | Comments |
|-|-|-|-|
| Targets | No - 7 | Yes according to code review status| |
| Blood oxygen saturations SPo2 Sats | No - 7 |Yes according to code review status||
| Pain scores | Yes | Yes according to code review status| Shifts are still depicted for 12 points, should be seven orange diamonds|
| Pain assessment frequency | Yes| Yes according to code review status|Shifts are still depicted for 12 points, should be seven orange diamonds|
| Mean Arterial Blood Pressure| No - 7|Yes according to code review status ||
| RASS Assessement| Yes |Yes according to code review status | Shifts are still depicted for 12 points, should be seven orange diamonds|
| RASS| No | Yes according to code review status| Recalculations seem random|
|Tidal Volume| No - 7 |Yes according to code review status||
| Airway Plan| Not enough data but suspect new rules|Yes according to code review status||
| Delirium | Yes|Yes according to code review status| Shifts are still depicted for 12 points, should be seven orange diamonds|
| Motor Block Assessment | Not enough data but suspect new rules|Yes according to code review status||
| DrEaMing| Not enough data but suspect new rules|Yes according to code review status||

