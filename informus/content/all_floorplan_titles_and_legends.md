\* **Frontend code updated July 24 but requires checking** \*

# All Floorplan titles and legends

To access individual floorplan select location and required tile/metric from Clinical Dashboard homepage

## Navigate

**1. Tabs on left**

- **Clinical Dashboard**
- Data for Improvement
- Critical Care Comms
- About us

**2. Location / Units**

- T03 Critical Care
- T06 Critical Care
- GWB Critical Care
- WMS Critical Care

**3. Overview of tiles / metrics**

- Bed Occupancy
- All targets set in ICU Navigators
- All patients Pain
- Patients on oxygen therapy SpO2 Saturations
- Patients on vasoactive drugs Mean Arterial BP
- Sedated patients RASS
- Patients on mandatory ventilation Tidal Volume
- Patients with a RASS -3 to +4 CAM-ICU
- All POM patients DrEaMing

![image](https://github.com/inform-us/requirements_specifications/assets/94536083/f4ceeba1-a5b4-45ed-867e-7d7435745fc7)

---

# All Floorplans contents:

- Unit top left
- Title top centre
- i and ? buttons bottom right
- Bed floorplan
- Legend to left of floorplan
- Back button bottom left

---

## Tile: Bed Occupancy

**Floorplan title: Bed Occupancy**

![image](https://github.com/inform-us/requirements_specifications/assets/94536083/23d194a0-ff09-4f26-b719-056d72ed389b)

---

## Tile: All targets set in ICU Navigator

**Floorplan title: Patients in critical care: All Targets set in ICU Navigators**

![image](https://github.com/inform-us/requirements_specifications/assets/94536083/c55bf8a5-af44-4750-b51b-b12af50dfd11)

---

## Tile: All patients Pain

**Floorplan title: Pain scores**

![image](https://github.com/inform-us/requirements_specifications/assets/94536083/2d0c069a-216a-4031-9dc1-2066a8cea500)

change 'on epidural' in legend to 'on epidural infusion'

## Tile: Patients on oxygen therapy SpO2 Saturations

**Floorplan title: Patients on oxygen therapy: SpO2 targets achieved**

![image](https://github.com/inform-us/requirements_specifications/assets/94536083/e306b7c7-6dcf-4c53-944e-6f67fa756177)

Add legend item - dark grey bed, label as 'incomplete data'

---

## Tile: Patients on vasoactive drugs Mean Arterial BP

**Floorplan title: Patients on intravenous vasoactive drugs: Mean Arterial Blood Pressure (MAP) targets achieved**

![image](https://github.com/inform-us/requirements_specifications/assets/94536083/71ad7bbb-5d20-4a92-aefd-bedbe08af5c3)

---

## Tile: Sedated patients RASS

**Floorplan title: Patients on sedation and mechanical ventilation: RASS Targets achieved**

![image](https://github.com/inform-us/requirements_specifications/assets/94536083/84251788-0f64-4a82-9a0f-a426df79ad8e)

---

## Tile: Patients on mandatory ventilation Tidal Volume

**Floorplan title: Patients on mandatory ventilation: Tidal Volume targets achieved (below 8ml/kg IBW**

![image](https://github.com/inform-us/requirements_specifications/assets/94536083/34b10f7f-6b12-4212-8e7a-aeb99d2ccc32)

Add legend item - dark grey bed, label as 'incomplete data'

---

## Tile: Patients with a RASS -3 to + 4 CAM-ICU

**Floorplan title: All patients with RASS score if > -3: CAM-ICU Delirium**

![image](https://github.com/user-attachments/assets/c00a4de3-8a86-486c-825d-0ea9542737d2)

Legend Labeling wording change: 

CAM-ICU positive (no RASS) to CAM-ICU positive (RASS overdue)

and 

CAM-ICU negative (no RASS) to CAM-ICU negative (RASS overdue)


## Tile: All POM patients DrEaMing

**Floorplan title: Eating and Drinking**

![image](https://github.com/user-attachments/assets/b996f030-82ae-42ed-b90d-3470129c45af)

Add IV as secondary label to legend. IV letters in shadow rectangle = 'IV in addition'

**Floorplan title: Mobilisation**

![image](https://github.com/user-attachments/assets/d1f4250e-11db-4c22-acf2-91144147d497)

Hover over 'In Bed' to pop up 'Reason's for not moblising' text.
_Note there are no other hover overs. Only in bed patients._

**Floorplan title: Documentation compliance**

Once code is changed to omit partial documentation as an option, removed amber filled bed 'partial documentation' in legend and change wording as per below. 

- DrEaMing Fully Documented - green-filled bed
- DrEaMing Documentation Incomplete- red-filled bed

- ![image](https://github.com/user-attachments/assets/7253fd06-78c0-4467-bbfc-7801125c3309)

## Tile: Airway Plan Completed

**Floorplan title: Airway Plan**

<img width="742" alt="image" src="https://github.com/user-attachments/assets/31cec9c4-7a68-4425-9d2e-3df51d219ea4">

## Tile: Type of Airway/Turning Plan

\*\*Floorplan title: Airway (Type/ Turning Plan/ DART call)

<img width="330" alt="image" src="https://github.com/user-attachments/assets/fda95e99-9da2-41f6-9281-563ba867b5a0">

## Updated Airway Plan Completed

**DLT** - Doctor led turn

**NLT** - Nurse led turn

**E** - Endotracheal tube

**T** - Tracheostomy

**L** - Laryngectomy

|                                                     | DART                                | DLT                                    | NLT                                    | E                                      | T                                      | L                                      | NONE                                  |
| --------------------------------------------------- | ----------------------------------- | -------------------------------------- | -------------------------------------- | -------------------------------------- | -------------------------------------- | -------------------------------------- | ------------------------------------- |
| (A) **DART (red border)**                           | X                                   | Red border, amber filling              | Red border, green filling              | Red border, - letter, grey filling     | Red border, T letter, grey filling     | Red border, L letter, grey filling     | Red border, very light blue filling   |
| (B) **DLT (amber border + filling)**                | Red border, amber filling           | X                                      | X                                      | Amber border + amber filling, - letter | Amber border + amber filling, T letter | Amber border + amber filling, L letter | Amber border + amber filling          |
| (B) **NLT (green border + filling)**                | Red border, green filling           | X                                      | X                                      | Green border + green filling, - letter | Green border + green filling, T letter | Green border + green filling, L letter | Green border + green filling          |
| (C) **E (- letter)**                                | Red border, grey filling, - letter  | Amber border + amber filling, - letter | Green border + green filling, - letter | Grey border + grey filling, - letter   | X                                      | X                                      | X                                     |
| (C) **T (T letter)**                                | Red border, grey filling, T letter  | Amber border + amber filling, T letter | Green border + green filling, T letter | X                                      | Grey border + grey filling, T letter   | X                                      | X                                     |
| (C) **L (L letter)**                                | Red border, grey filling, L letter  | Amber border + amber filling, L letter | Green border + green filling, L letter | X                                      | X                                      | Grey border + grey filling, L letter   | X                                     |
| (C) **NONE (grey border, very light blue filling)** | Red border, very light blue filling | Amber border + amber filling           | Green border + green filling           | X                                      | X                                      | X                                      | Grey border + very light blue filling |

Cannot >1 of E, T, L NONE at same time

DLT trumps NLT

Can have one from each section (A) (B) (C), e.g, DART, DLT, E

Can have section (A)&(B) or (A)&(C) or (B)&(C) e.g, DART & DLT, DLT & E

Can have only from section (A), i.e, only dart

Can have only from section (B), e.g, only DLT

Can have only from section (C), e.g, only E


**Floorplan title: Motor Block Assessment**

Legend 

GREEN: Latest motor block 0-1

AMBER: Latest motor block 2

RED: Latest motor block 3

Overdue Assessment

No epidural infusion in the last 12hrs

Empty bed




