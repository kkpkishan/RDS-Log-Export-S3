# **Reducing your bill for AWS RDS cloudwatch**
In a traditional on-premises database, the DB logs reside on the file system itself. But in the case of AWS managed DB service, it doesn’t provide host access to the database logs on the file system of the DB instance.

So the question is how to get the logs and perform analysis or troubleshooting?

AWS RDS allows configuring and export database logs to Amazon CloudWatch logs. Once it is exported, one can perform real-time analysis of the log data, store the data in highly durable storage, and manage the data with the CloudWatch Logs Agent.

![](Aspose.Words.85af6788-5579-469c-8d1b-802c9d30d5d8.001.png)

The cost calculation for RDS logs exporting to Amazon Cloudwatch log group is as below.

![](Aspose.Words.85af6788-5579-469c-8d1b-802c9d30d5d8.002.png)

This is good for most of the cases.

There are two perspective for RDS CloudWatch logs majority

1. Charges for ingested data in GB/TB etc
1. Charges for storage logs in GB/TB etc

Charges for ingested data are significantly higher than the charges for storage.
# For 100GB the calculation of the charges are
100 GB x 0.67 USD = 67.00 USD

**Standard Logs Data Ingested cost: 67.00 USD**

**CloudWatch Logs Data Ingested tiered pricing cost: 0 USD**

100.00 GB per month x 0.15 Storage compression factor x 1 Logs retention factor x 0.03 USD = 0.45 USD

**Standard/Vended Logs data storage cost: 0.45 USD**

**Logs delivered to S3 Data Ingested cost: 0 USD**

**Logs converted to Apache Parquet format cost: 0 USD**

67.00 USD + 0.45 USD = 67.45 USD

**CloudWatch Logs Ingested and Storage cost (monthly): 67.45 USD**

# For 1000GB the calculation of the charges are
1,000 GB x 0.67 USD = 670.00 USD

**Standard Logs Data Ingested cost: 670.00 USD**

**CloudWatch Logs Data Ingested tiered pricing cost: 0 USD**

1,000.00 GB per month x 0.15 Storage compression factor x 1 Logs retention factor x 0.03 USD = 4.50 USD

**Standard/Vended Logs data storage cost: 4.50 USD**

**Logs delivered to S3 Data Ingested cost: 0 USD**

**Logs converted to Apache Parquet format cost: 0 USD**

670.00 USD + 4.50 USD = 674.50 USD

**CloudWatch Logs Ingested and Storage cost (monthly): 674.50 USD**

# For 10000GB the calculation of the charges are
10,000 GB x 0.67 USD = 6,700.00 USD

**Standard Logs Data Ingested cost: 6,700.00 USD**

**CloudWatch Logs Data Ingested tiered pricing cost: 0 USD**

10,000.00 GB per month x 0.15 Storage compression factor x 1 Logs retention factor x 0.03 USD = 45.00 USD

**Standard/Vended Logs data storage cost: 45.00 USD**

**Logs delivered to S3 Data Ingested cost: 0 USD**

**Logs converted to Apache Parquet format cost: 0 USD**

6,700.00 USD + 45.00 USD = 6,745 USD

**CloudWatch Logs Ingested and Storage cost (monthly): 6,745.00 USD**

Let us summarise it 


|**Size in GB**|**Cost for Storage USD**|**Cost for Data ingested USD**|
| :- | :- | :- |
|100|0.45|67|
|1000|4.50|670|
|10000|45.00|6700|
As mentioned it is good for most of the cases. Cloudwatch provides built-in analysis tools and integration to other services.

In case the cost is significantly high for the logs ingested we have one alternative approach available.

Remember, this is an alternative approach, It may or may not be better for your case. Check and understand the pros and cons.
# The approach 
The approach is simple but logical.

Though in case of Amazon RDS, one can not access the file system directly, AWS has provided APIs to access and download the logs files.

We will write a Lambda function which calls the API to download the file and dump it into the S3 Bucket. This will be performed periodically.

Please follow the below instructions.

![](Aspose.Words.85af6788-5579-469c-8d1b-802c9d30d5d8.003.png)

For simplicity to create lambda functions, CloudFormation templates are created. Please use the templates.

1. **Create Option Group**
- Under Options section, click on Add option button.
- Under “SERVER\_AUDIT\_EVENTS\*” option, enter the values that you want to audit i.e. CONNECT, QUERY, QUERY\_DDL, QUERY\_DML, QUERY\_DCL, QUERY\_DML\_NO\_SELECT. If you want to log all the queries run on your tables, just enter QUERY in this field.
- Set “Yes” for Apply Immediately. Click on Add Option.

2. **Create Parameter Group**
- Under Parameter, we will edit the certain parameters and set the following values:
- Edit parameter: “log\_output” ⇒ Change its value from TABLE to FILE
- Edit parameter: “slow\_query\_log” ⇒ Change its value from BLANK to 1
- Edit parameter: “general\_log” ⇒ Change its value from BLANK to 1

3. **Run the Cloudformation Template.** 

https://github.com/kkpkishan/RDS-Log-Export-S3/blob/main/cf-template-other.yaml

The cost saving

![](Aspose.Words.85af6788-5579-469c-8d1b-802c9d30d5d8.004.png)

# Conclusion
One can save significant cost with this approach.

One might need additional software or athena to analyse the logs.

Team ElectroMech Cloudtech Pvt. Ltd.

- Kishan Khatrani (Head of AWS practise)
- Nilesh Vaghela (CEO)


