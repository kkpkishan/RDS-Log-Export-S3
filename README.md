# How to Automatically Export AWS RDS  Logs to S3 Bucket 
![Blank diagram](https://user-images.githubusercontent.com/38881285/187905234-c2298490-9179-421b-adef-3e8d9427eb92.png)

<h4> Why not just use CloudWatch?</h4> 
<p>For MariaDB, MySQL, Oracle, PostgreSQL, and MS SQL Server, AWS allows you to automatically publish database log files to CloudWatch Logs. However, CloudWatch Logs is not free. In fact, it can be quite expensive. For a moderately sized production database publishing ~2 TB of log files per month, the CloudWatch costs will likely exceed $1000 in data transfer alone.

Instead, you can run this script as an AWS Lambda function (see below) multiple times per hour, and still likely be in the free-tier so far as costs go.

If you have a low volume of data, I still recommend using CloudWatch just for simplicity's sake.</p>

<h4> 1) Create Option Group </h4>
 <br>- Under Options section, click on Add option button.</br>
 <br>- Under “SERVER_AUDIT_EVENTS*” option, enter the values that you want to audit i.e. CONNECT, QUERY, QUERY_DDL, QUERY_DML, QUERY_DCL, QUERY_DML_NO_SELECT. If you want to log all the queries run on your tables, just enter QUERY in this field.</br>
 <br>- Set “Yes” for Apply Immediately. Click on Add Option.</br>
<h4> 2) Create Parameter Group </h4>
 <br>- Under Parameter, we will edit the certain parameters and set the following values:</br>
 <br>- Edit parameter: “log_output” ⇒ Change its value from TABLE to FILE</br>
 <br>- Edit parameter: “slow_query_log” ⇒ Change its value from BLANK to 1</br>
 <br>- Edit parameter: “general_log” ⇒ Change its value from BLANK to 1</br>
 
<h4> 3) Run the Cloudformation Template </h4>
