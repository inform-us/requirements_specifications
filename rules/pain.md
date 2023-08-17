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
> Verbal Pain Scale (at rest) - Row ID 3040104280

> Verbal Pain Scale (at movement) - Row ID 3040104281
> 




* ### Critical Care Observation Tool (CPOT) - components
> Facial Expression    -                           			Row ID 3040104654

> Body Movements       -                        		   	Row ID 3040104655 

> Compliance with Ventilator     -                			Row ID 3040104656


---


## Table: equivalence between VPS & CPOT  
| Classification | VPS (rest/move) | CPOT | Transformed CPOT | Validity time | Test |
|-|-|-|-|-|-|
| Unable to assess with 'other' filled | 0 | ?? | ?? | 5 hours | ?? |
| No | 0 | 0 | 0 | 5 hours | ?? |
| Mild | 1 | 1-2 | 1 | 5 hours | ?? |
| Moderate | 2 |  3-4 | 2 | 75 minutes | ??|
| Severe | 3 | 5-6 | 3| 75 minutes | ?? |
| Very severe | 4 | 7-8 | 4 | 75 minutes | ?? |

8. If no valid score in the current epoch, then forward fill, using above validity (time) rules (i.e. if green forward fill for 5 hours, if amber or red 75 minutes. 
