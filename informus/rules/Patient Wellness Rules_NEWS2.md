# DRAFT of beginning of  Rules for Patient Wellness Question (Martha's Rule) linked to NEWS2

## EPIC

The NEWS2 score is an ealry warning score measuring physiological deterioration. It looks at the following parameters: respiratory (respiratory rate, SpO2, supplemental oxygen), cardiovascualr (systoloic blood pressure, pulse rate), neurological (consciousl level) and temperature. It ranges from 0-20. It is usually grouped by severity into the following: 0–2, 3–4, 5–6 and 7+. A numerical trigger for escalation is commonly a NEWS2 score = 5. 

https://www.rcp.ac.uk/media/a4ibkkbf/news2-final-report_0_0.pdf


### Group ID 

National Early Warning Score_2 (NEWS2)

Group ID: G UCLH NEWS SCORING [304080160]	

### Row ID 

Row ID: R NEWS SCORE RESULT - DISPLAYED [28315]
- this is a calculated score
- integer
- range 0-20


NEWS2 'Action Taken' - not currently used for this metric
RowID: R NEWS ACTION TAKEN [6503]

NEWS2 'How does the patient feel?'

Row ID: R UCLH NEWS PATIENT FEEL [304080162]
- drop down with with four options (better than before / the same / worse / don't know)
- option for free text


General information about metric (e.g. location, components, group or summative score etc)
metric output (e.g. numerical (integer / decimal), drop down, range selection, free text etc)
Are there corresponding targets?
EPIC Flowsheets
ABC metric [ID XXXX for Group or summative score if applicable]
ABC metric - Row ID XXXX
ABC metric [component if applicable] - Row ID XXXX
Flowsheet	Row ID	Manual/Automatic/Calculated Input	Comments	Expected documentation frequency
PDF - ABC metric user interface sequence



## ELIGIBILITY
All patients in 10 pilot wards, plus third roll out of wards, eventually Trust roll out. 
VALIDITY
for XYZ calculation (e.g. 1 hour epoch) used for which part of user interface (e.g. floorplan, individual chart & SPC)

## CLASSIFICATION

Go through each metric in sequence and which charts this data feeds into.

### [A] ABC Measurement Interval

E.G. Feeds into (i) front tile - 24 hour rolling window and (ii) SPC interval charts.

### [B] ABC metric front tile calculation

### [C] Floorplan labelling

### [D] Classification Rules: Individual patient chart

## [E] SPC CHARTS
ABC SPC CHARTS (refer to XYZ metric in classification

Calendar day defined as 00:00 - 23:59
Week defined as Monday 00:00 – Sunday 23:59

### Chart 1 [Patient chart]
Proportion of moderate or severe pain scores – weekly chart

Operational definition = of the documented pain scores in EPIC, what proportion are moderate or severe on a weekly basis?

### Chart 2

These are weekly percentage (p-charts) SPC
Week defined a Monday 00:00 – Sunday 23:59
