# How to Automatically Export AWS RDS Audit Logs to S3 Bucket instance
![Blank diagram](https://user-images.githubusercontent.com/38881285/187905234-c2298490-9179-421b-adef-3e8d9427eb92.png)

1) Create Option Group
 - Under Options section, click on Add option button.
 - Under “SERVER_AUDIT_EVENTS*” option, enter the values that you want to audit i.e. CONNECT, QUERY, QUERY_DDL, QUERY_DML, QUERY_DCL, QUERY_DML_NO_SELECT. If you want to log all the queries run on your tables, just enter QUERY in this field.
 - Set “Yes” for Apply Immediately. Click on Add Option.
 2) Create Parameter Group 
 - Under Parameter, we will edit the certain parameters and set the following values:
 - Edit parameter: “log_output” ⇒ Change its value from TABLE to FILE
 - Edit parameter: “slow_query_log” ⇒ Change its value from BLANK to 1
 - Edit parameter: “general_log” ⇒ Change its value from BLANK to 1
 
 3) Run the Cloudformation Template 
