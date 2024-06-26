# Accessing Tabular Data in the Data Science Desktop 

## Updated March 2024

DBForge is a programme for looking at databases

*Note There is a wiki about DB forge access called common tasks and how tos on the git hub repository. Lots of other common tasks too.*
*This is also on Read me on Repo uclvldddtaeps02.xuclh.nhs.uk*

--------

* On the NHS desktops you need to start with citrix login which is on the bottom right hand corner of the screen. 
* Using the Data Science Desktop, on citrix, open dbForge Studio for PostgreSQL > Devart, DB Forge in the windows drop down
* IF 'trial period expired' message, select 'Use Express' and re-open dbForge
* Enter the database information when prompted using the following:


> Host: UCLVLDDDTAEPS02
Port: 5432
User: Your EMAP username
Password: Your EMAP password
Database: uds

*note the `Test Connection` button shows whether you are able to successfully connect*
 
* After connection you may be met with another an optional update for dbForge - reply with 'Ask Later'
 
* You can now start viewing tabular data. This is possible via SQL query (New SQL tab at the top left) or graphically through the GUI (FYI for not developers). 
 
* For the graphical GUI method select the drop-down arrow next to the 'uds' entry in the panel at the top left of the screen > scroll down to the 'informus' entry > select drop-down arrows next to 'informus' > select'Tables'. 

You should see something like
  
You can now view the data in any of these tables by double-clicking on the name of the table. For general browsing, please select 'read-only' when prompted, unless you intend to alter data within the tables.
Once the tables are loaded you are able to filter by any of the columns shown. 

> *More interesting/advanced queries can be performed by manually writing SQL queries via with 'New SQL' and 'Execute' buttons in the top left*

> *Remember that our tables are in the 'informus' database - an example query to show all of the hourly SpO2 data in descending order (by time written to the database) is given by SELECT * FROM informus.oxygen ORDER BY log_dt DESC; again, when prompted please select the 'read-only' view!*

----------

## Instructions for using Tables in DB forge to investigate data

Inform_us is production 
Inform_us staging is staging
*Note that the data that is being worked on in staging, will not be available in the tables.*

* Within these open tables you will see all the data on each metric. 
* Double click on a metric and you open up all the stored data we store daily (Note this is processed, not raw EMAP data).
* You can sort the data by clicking on the metric heading at top, e.g. like excel.
* This will show 1000 rows per page
* Scroll between rows with arrows at the bottom of the table.
* Scroll between pages of 1000 with the arrows at the top of the table.
* 
## To filter
* You can filter by MRN or bay and by date etc to look at a specific subset of the data.
* e.g. to find a patient for a certain period of time go to data tab > quick filter > condition >  type  new mrn >  select + and 

## To export
* Right click on the table > export to CSV or other formats > select field seperater >comma > select columns you want (all) or can choose a range of rows
* You can also highlight particular rows in the table and right-click to export those rows. 
*Note we could actually build run charts using these data* 

> **A data export should be done twice a year, in January and June for all metrics** 




