# SkipTheDishs Hackathon
# A Cloud Based Scalable Architecture

## About the project
This project is about a generic architecture for scalable applications hosted on Cloud.
The cloud provider chosen is Amazon because they have numerous products, for all kind of needs, and all of then fully manageable and auto-scalable, so your developer team can focus on developing awesome products instead of managing clusters, products updates and dealing with highly spikes of requests/users and downtimes.

The project is based on Lambda architecture, where you have a data-pipeline of streaming processing, to delivery near real time responses to the users and your analysis team(BI or data science) and another data-pipeline of batch processing where you consolidate and process large amount of data and deliver trustful enrichment data for all teams and applications.

## Data Pipeline - Streaming Layer 
![Fast Data Layer](https://github.com/edumello/SkipTheDishes-scalable-architecture/blob/master/fast-data.JPG?raw=true)
The Fast-Data layer covers the near real time data produced by applications, web sites and logs.

The non-structured data, produced by internal and external applications, are received by APIs that must have fast response times with data from a memory-cached database, the DynamoDB, which is integrated with an ElasticSearch to provide free-text format queries.

The applications data is sent to Kinesis, to support high spikes of millions requests, and from Kinesis to:

- The Kinesis Firehose, in raw format to be stored at a S3 Data Lake for future analysis and insights.

- EMR, a fully-manageable and auto-scalable Spark Streaming cluster, to consolidate and prepare the data for a structured  data warehouse database. The data can be consumed by any traditional BI tool to display near-real-time data analysis.

## Data Pipeline - Batch Layer 
![Batch Data Layer](https://github.com/edumello/SkipTheDishes-scalable-architecture/blob/master/batch-layer.JPG?raw=true)
The Batch Layer provides large processing power to consolidate, transform and analyse new and historical data.

On a scheduled time the data is collected from all sources to EMR instances where it is processed using Spark-Dataframe jobs to join all kinds of data, providing data enrichment  and preparing the data in many aggregations levels and formats.
Once the spark pipeline is finished, the data will be stored on:

- S3 Data Lake for Data Science Team do analysis and get insights from the Data.

- Redshift, to provide structured data for traditional applications, like BI Tools and websites

- ElasticSearch to update DynamoDB and low-latency databases
