# Create Custom Reports and Analyze AppStream 2\.0 Usage Data<a name="configure-custom-reports-analyze-usage-data"></a>

Amazon Athena is a serverless, interactive query service that you can use to analyze data stored in your S3 buckets using standard SQL queries\. You can use Athena to aggregate your usage reports or generate other types of custom reports\. 

**Topics**
+ [Create an AWS Glue Crawler](#configure-custom-reports-create-crawler)
+ [Create a Data Catalog by Using the AWS Glue Crawler](#configure-custom-reports-create-data-catalog)
+ [Create and Run Athena Queries](#configure-custom-reports-create-run-athena-queries)
+ [Working with Athena Queries](#configure-custom-reports-example-sql-queries)

## Create an AWS Glue Crawler<a name="configure-custom-reports-create-crawler"></a>

AWS Glue is a fully managed extract, transform, and load \(ETL\) service that lets you create a database from your Amazon S3 data and query that database by using Athena\. This database is also referred to as an AWS Glue Data Catalog\. An AWS Glue crawler can automatically detect the schema of your Amazon S3 data and create the corresponding database and tables\. AppStream 2\.0 provides an AWS CloudFormation template that you can use to create the necessary AWS Glue resources\. 

**Important**  
Completing the steps in the following procedure creates an AWS Glue crawler\. However, these steps don’t start the crawler\. To start the crawler, you must perform the steps in the next procedure\. For more information about AWS Glue crawlers, see [Defining Crawlers](https://docs.aws.amazon.com/glue/latest/dg/add-crawler.html)\.

**To create an AWS Glue crawler**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. Choose the AWS Region for which you have subscribed to usage reports\.

1. In the navigation pane, choose **Usage Reports**, and verify that usage reports logging is enabled\.

1. On the **Report Details** tab, in the paragraph next to **Analytics**, choose the **CloudFormation template** link\.

   Choosing the link opens the AWS CloudFormation console, where you can review the parameters of the AWS CloudFormation stack specified by the template before you run it\. The template, when run, creates an AWS Glue crawler and several sample Athena queries\.

1. On the **Specify Details** page, next to **ScheduleExpression**, either keep the default value or specify a different cron expression value for the frequency that you want to run the crawler\. Do not change any other default value\. When you're done, choose **Next**\.

   By default, the crawler is scheduled to run on a daily basis, but you can configure the crawler to run weekly, monthly, or on another frequency\. For information about cron syntax, see [Cron Expressions](https://docs.aws.amazon.com/AmazonCloudWatch/latest/events/ScheduledEvents.html#CronExpressions)\.

1. On the **Options** page, keep the default values, and choose **Next**\.

1. On the **Review **page, select the check box next to "I acknowledge that AWS CloudFormation might create IAM resources with custom names," and then choose **Create**\.

   You must have sufficient AWS Glue and AWS Identity and Access Management \(IAM\) permissions to create and run the AWS CloudFormation stack\. If you don't have the required permissions, ask your AWS account administrator either to perform these steps in your account or to grant you the following permissions\.

   ```
   {
       "Version": "2012-10-17",
       "Statement": [
           {
               "Effect": "Allow",
               "Action": [
                   "athena:CreateNamedQuery",
                   "athena:BatchGetNamedQuery",
                   "athena:GetNamedQuery",
                   "athena:StartQueryExecution",
                   "athena:GetQueryResults",
                   "athena:GetQueryExecution",
                   "athena:ListNamedQueries",
                   "cloudformation:DescribeStacks",
                   "cloudformation:GetStackPolicy",
                   "cloudformation:DescribeStackEvents",
                   "cloudformation:CreateStack",
                   "cloudformation:GetTemplate",
                   "cloudformation:ListChangeSets",
                   "cloudformation:ListStackResources",
                   "iam:GetRole",
                   "iam:CreateRole",
                   "iam:GetRolePolicy",
                   "s3:GetBucketLocation",
                   "s3:ListBucketMultipartUploads",
                   "s3:ListBucket",
                   "s3:ListMultipartUploadParts",
                   "s3:PutObject",
                   "s3:GetObject",
                   "s3:AbortMultipartUpload"
               ],
               "Resource": [
                   "arn:aws:iam::*:role/AppStreamUsageReports-AppStreamUsageReportGlueRole*",
                   "arn:aws:cloudformation:*:*:stack/AppStreamUsageReports/*",
                   "arn:aws:athena:*:*:workgroup/primary",
                   "arn:aws:s3:::aws-athena-query-results-*"
               ]
           },
           {
               "Effect": "Allow",
               "Action": [
                   "iam:AttachRolePolicy",
                   "iam:PutRolePolicy",
                   "s3:GetObject",
                   "s3:ListBucket"
               ],
               "Resource": [
                   "arn:aws:s3:::appstream-logs-*",
                   "arn:aws:iam::*:role/AppStreamUsageReports-AppStreamUsageReportGlueRole*"
               ]
           },
           {
               "Effect": "Allow",
               "Action": [
                   "iam:PassRole"
               ],
               "Resource": [
                   "arn:aws:iam::*:role/AppStreamUsageReports-AppStreamUsageReportGlueRole*"
               ],
               "Condition": {
                   "StringEquals": {
                       "iam:PassedToService": "glue.amazonaws.com"
                   }
               }
           },
           {
               "Effect": "Allow",
               "Action": [
                   "cloudformation:GetTemplateSummary",
                   "glue:GetResourcePolicy",
                   "glue:GetCrawlers",
                   "glue:BatchGetCrawlers",
                   "glue:GetClassifiers",
                   "glue:CreateClassifier",
                   "glue:ListCrawlers",
                   "glue:GetTags",
                   "glue:GetCrawlerMetrics",
                   "glue:GetClassifier",
                   "tag:GetResources"
               ],
               "Resource": "*"
           },
           {
               "Effect": "Allow",
               "Action": "athena:RunQuery",
               "Resource": "arn:aws:athena:*:*:workgroup/primary"
           },
           {
               "Effect": "Allow",
               "Action": [
                   "glue:GetTables",
                   "glue:GetPartitions",
                   "glue:GetTable"
               ],
               "Resource": [
                   "arn:aws:glue:*:*:table/appstream-usage/*",
                   "arn:aws:glue:*:*:database/appstream-usage",
                   "arn:aws:glue:*:*:catalog"
               ]
           },
           {
               "Effect": "Allow",
               "Action": [
                   "glue:GetDatabase",
                   "glue:CreateDatabase",
                   "glue:GetDatabases"
               ],
               "Resource": [
                   "arn:aws:glue:*:*:database/appstream-usage",
                   "arn:aws:glue:*:*:catalog"
               ]
           },
           {
               "Effect": "Allow",
               "Action": [
                   "glue:GetCrawler",
                   "glue:StartCrawler",
                   "glue:CreateCrawler"
               ],
               "Resource": "arn:aws:glue:*:*:crawler/appstream-usage*"
           },
           {
               "Effect": "Allow",
               "Action": "glue:GetCatalogImportStatus",
               "Resource": "arn:aws:glue:*:*:catalog"
           }
       ]
   }
   ```

## Create a Data Catalog by Using the AWS Glue Crawler<a name="configure-custom-reports-create-data-catalog"></a>

The AWS Glue crawler, when run, creates a Data Catalog and schema that are mapped to the structure of your sessions and applications reports\. Each time a new report is stored in your Amazon S3 bucket, you must run the crawler to update your AWS Glue Data Catalog with the data from the new report\. 

**Note**  
Charges may apply to the running of your AWS Glue crawler\. For more information, see [AWS Glue Pricing](https://aws.amazon.com/glue/pricing/)\.

1. Open the AWS Glue console at [https://console\.aws\.amazon\.com/glue/](https://console.aws.amazon.com/glue/)\.

1. Choose the AWS Region for which you have subscribed to usage reports\.

1. Select the check box next to the crawler named **appstream\-usage\-sessions\-crawler**, and then choose **Run crawler**\. Repeat this step for the crawler named **appstream\-usage\-apps\-crawler**\. 

   Performing these steps runs the crawlers and schedules them to run automatically according to the schedule specified in the AWS CloudFormation stack\. 

1. After both crawlers finish running, in the navigation pane, choose **Databases**\. A database named **appstream\-usage**, which represents your usage reports, displays\. This database is an AWS Glue Data Catalog that was created when **appstream\-usage\-sessions\-crawler** and **appstream\-usage\-apps\-crawler** were run\.

1. To view the tables in the database, choose **appstream\-usage**, **Tables**\. Two tables, **applications** and **sessions**, which represent your applications and sessions usage reports respectively, display\. Choose either table to view its schema\.

   You can now query these tables in Athena by using SQL\.

## Create and Run Athena Queries<a name="configure-custom-reports-create-run-athena-queries"></a>

To query your usage reports by using Athena, perform the following steps\.
**Note**  
Charges may apply to Athena queries that you run\. For more information, see [Amazon Athena Pricing](https://aws.amazon.com/athena/pricing/)\.

1. Open the Athena console at [https://console\.aws\.amazon\.com/athena/](https://console.aws.amazon.com/athena/home)\.

1. Under **Database**, choose **appstream\-usage**\.

1. In the query pane, enter a SQL query, and choose **Run query**\.

## Working with Athena Queries<a name="configure-custom-reports-example-sql-queries"></a>

This section provides SQL queries that you can run in Athena to analyze the usage reports data in your Amazon S3 bucket\.

To create a consolidated report of all sessions in a given month, run the following query:

```
SELECT *
FROM "appstream-usage"."sessions"
WHERE year='four-digit-year'
AND month='two-digit-month'
```

You can also perform join operations between the **applications **and **sessions** tables in your query\. For example, to view the distinct users who launched each application in a given month, run the following query:

```
SELECT DISTINCT apps.application_name, sessions.user_id
FROM "appstream-usage"."applications" apps
   INNER JOIN "appstream-usage"."sessions" sessions ON (apps.user_session_id = sessions.user_session_id AND sessions.year='four-digit-year' AND sessions.month='two-digit-month')
WHERE apps.year='four-digit-year'
  AND apps.month='two-digit-month'
ORDER BY 1, 2
```

Athena query results are stored as \.csv files in an Amazon S3 bucket in your account that is named `aws-athena-query-results-account-id-without-hyphens-region-code`\. For ease in locating query results, choose **Save as** and provide a name for your query before you run it\. You can also choose the download icon in the **Athena Results** pane to download the results of the query as a \.csv file\.

To enhance performance and reduce costs, Athena uses partitioning to reduce the amount of data scanned in queries\. For more information, see [Partitioning Data](https://docs.aws.amazon.com/athena/latest/ug/partitions.html)\. Usage reports are partitioned in your Amazon S3 buckets by year, month, and day\. You can restrict your queries to certain date range partitions using the **year**,** month**, and **day** fields as conditions in your queries\. For example, the following query ingests only the sessions reports for the week of May 19, 2019\.

```
SELECT SUBSTRING(session_start_time, 1, 10) AS report_date, 
    COUNT(DISTINCT user_session_id) AS num_sessions
FROM "appstream-usage"."sessions"
WHERE year='2019'
   AND month='05'
   AND day BETWEEN '19' and '25'
GROUP BY 1
ORDER BY 1
```

In contrast, the following query produces identical results, but because it isn't restricted to any partitions, it ingests all sessions reports stored in your Amazon S3 bucket\.

```
SELECT SUBSTRING(session_start_time, 1, 10) AS report_date, 
    COUNT(DISTINCT user_session_id) AS num_sessions
FROM "appstream-usage"."sessions"
WHERE session_end_time BETWEEN '2019-05-19' AND '2019-05-26'
GROUP BY 1
ORDER BY 1
```

If a session spans more than one day, the session and application records appear in the sessions and applications reports, respectively, corresponding to the day in which the session ended\. For this reason, if you need to find records that relate to all sessions that were active during a given date range, consider expanding the partition set of your query by the maximum session length you have configured for your fleets\.

For example, to view all sessions that were active for a given fleet during a calendar month, where the fleet had a maximum session duration of 100 hours, run the following query to expand your partition set by five days\.

```
SELECT *
FROM "appstream-usage"."sessions"
WHERE fleet_name = 'fleet_name'
   AND session_start_time BETWEEN '2019-05-01' AND '2019-06-01'
   AND year='2019'
   AND (month='05' OR (month='06' AND day<='05'))
ORDER BY session_start_time
```

The AWS CloudFormation template that created the AWS Glue crawlers also created and saved several sample queries in your Athena account that you can use to analyze your usage data\. These sample queries include the following:
+ Aggregated monthly session report
+ Average session length per stack
+ Number of sessions per day
+ Total streaming hours per user
+ Distinct users per app

To use any of these queries, perform the following steps\.

1. Open the Athena console at [https://console\.aws\.amazon\.com/athena/](https://console.aws.amazon.com/athena/)\.

1. Choose **Saved Queries**\. The five queries noted before this procedure should display\. The name of each query begins with "AS2\." For example, "AS2\_users\_per\_app\_curr\_mo\."

1. To run a query, choose the query name rather than the option next to the name\.

1. The text of the query appears in the query pane\. Choose **Run query**\.

To view these queries in a separate AWS CloudFormation template, see [athena\-sample\-queries\-appstream\-usage\-data\_template\.yml](https://docs.aws.amazon.com/code-samples/latest/catalog/cloudformation-appstream2-athena-sample-queries-appstream-usage-data_template.yml.html) in the *AWS Code Sample Catalog\.*