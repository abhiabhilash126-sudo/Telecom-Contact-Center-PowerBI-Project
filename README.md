# Telecom-Contact-Center-PowerBI-Project
This is a Telecom contact center Power BI Project, data consists of a year.
The data set for this project is a SQL 'Telecom Contact Center Data Ware House' database which is another project I made
This report is meant for showing the Contact Center Performance: Overall, Daily, Weekly, Site, Manager, Team Leader and finally Agent
There are few rows called unknown, any missing employee in employee table will be marked as unknown, another is N/A assigned for Abandoned calls as call never came to the contact center
<br>
To view the report, please download the file and open to see all the reports included in the file, DO NOT refresh as the data source is a local in prem which will throw an error if refreshed.

DAX formulas used:

Total Calls = COUNTROWS(fact_calls)
<br> <br>
Answered Calls = CALCULATE([Total Calls],fact_calls[call_status]="Answered") 
<br><br>
Answered Rate = DIVIDE([Answered Calls],[Total Calls]) 
<br><br>
Abandoned Calls = CALCULATE([Total Calls],fact_calls[call_status]="Abandoned") 
<br><br>
Abandoned Rate = DIVIDE([Abandoned Calls],[Total Calls]) 
<br><br>
Resolved Calls = CALCULATE([Total Calls],fact_calls[resolution_status]="Resolved") 
<br><br>
Resolution Rate = DIVIDE([Resolved Calls],[Answered Calls]) 
<br><br>
Missed Calls = CALCULATE([Total Calls],fact_calls[call_status]="Missed") 
<br><br>
Missed Call Rate = DIVIDE([Missed Calls],[Total Calls]) 
<br><br>
AHT seconds = CALCULATE(AVERAGEX(fact_calls,fact_calls[call_duration_seconds]+ fact_calls[hold_time_seconds]+fact_calls[acw_time_seconds]),fact_calls[call_status] = "Answered") 
<br><br>
AHT Duration = VAR TotalSeconds = [AHT seconds] RETURN FORMAT(TotalSeconds/86400,"hh:mm:ss") 
<br><br>
FCR % = DIVIDE(CALCULATE([Total Calls],fact_calls[fcr_flag] = 1),[Answered Calls]) 
<br><br>
Transfer Rate = DIVIDE(CALCULATE([Total Calls],fact_calls[transfer_flag] = 1),[Answered Calls]) 
<br><br>
Complaint Rate = DIVIDE(CALCULATE([Total Calls],fact_calls[complaint_flag] = 1),[Total Calls]) 
<br><br>
Escalation Rate = DIVIDE(CALCULATE([Total Calls],fact_calls[escalation_flag] = 1),[Answered Calls]) 
<br><br>
Promoters = CALCULATE([Total Calls],fact_calls[nps_score] >=9) 
<br><br>
Detractors = CALCULATE([Total Calls],fact_calls[nps_score] <= 6) 
<br><br>
NPS = VAR ValidResponse = CALCULATE([Total Calls], NOT ISBLANK(fact_calls[nps_score])) RETURN DIVIDE([Promoters]-[Detractors],ValidResponse) 
<br><br>
CSAT% = DIVIDE(AVERAGE(fact_calls[csat_score]),5)
