# How to Automatically Export AWS RDS  Logs to S3 Bucket 
![Blank diagram](https://user-images.githubusercontent.com/38881285/187905234-c2298490-9179-421b-adef-3e8d9427eb92.png)

<h4> 1) Create Option Group </h4>
 <br>- Under Options section, click on Add option button.</br>
 <br>- Under “SERVER_AUDIT_EVENTS*” option, enter the values that you want to audit i.e. CONNECT, QUERY, QUERY_DDL, QUERY_DML, QUERY_DCL, QUERY_DML_NO_SELECT. If you want to log all the queries run on your tables, just enter QUERY in this field.</br>
 <br>- Set “Yes” for Apply Immediately. Click on Add Option.</br>
<h4> 2) Create Parameter Group </h4>
 <br>- Under Parameter, we will edit the certain parameters and set the following values:</br>
 <br>- Edit parameter: “log_output” ⇒ Change its value from TABLE to FILE</br>
 <br>- Edit parameter: “slow_query_log” ⇒ Change its value from BLANK to 1</br>
 <br>- Edit parameter: “general_log” ⇒ Change its value from BLANK to 1</br>
 
<h4> 3) Run the Cloudformation Template <h4>
