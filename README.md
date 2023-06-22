




# 📈 Stock Market Analysis End-to-End Data Engineering Project 🚀

Welcome to the Stock Market Analysis End-to-End Data Engineering Project! <br>
This project leverages various technologies and tools like Kafka, Python, Amazon AWS EC2, Athena, S3 buckets, and Spark to perform comprehensive analysis on stock market data. 

## Prerequisites 🛠️

Make sure you have the following prerequisites installed and configured:

- Python
- Apache Kafka: Install and set up Kafka by following the official documentation: https://kafka.apache.org/documentation/. <br>
    (Use the latest compatible versioN and install corresponding JDK for running Kafka)
- Amazon AWS Account: Create an AWS account if you don't have one already: https://aws.amazon.com/.
1. S3 (Simple Storage Service)
2. Athena
3. Glue Crawler
4. Glue Catalog
5. EC2

## Dataset Used

Here is the dataset used : https://github.com/darshilparmar/stock-market-kafka-data-engineering-project/blob/main/indexProcessed.csv

## Project Setup ⚙️

1. Clone the repository:

   ```
   git clone https://github.com/your_username/stock-market-analysis.git
   ```

2. Navigate to the project directory:

   ```
   cd stock-market-analysis
   ```

## Data Pipeline Configuration 🔄

In this section, we will configure the data pipeline using Kafka, AWS S3 buckets, and Amazon Athena.

1. Start ZooKeeper and Kafka server:

   ```
   # Start ZooKeeper
   zookeeper-server-start.sh config/zookeeper.properties

   # Start Kafka server
   kafka-server-start.sh config/server.properties
   ```

2. Create a Kafka topic:

   ```
   kafka-topics.sh --create --topic stock_data --bootstrap-server localhost:9092 --partitions 1 --replication-factor 1
   ```

3. Configure AWS credentials:

   ```
   export AWS_ACCESS_KEY_ID=<your-access-key-id>
   export AWS_SECRET_ACCESS_KEY=<your-secret-access-key>
   ```

4. Create an S3 bucket for storing stock market data. Note down the bucket name for later use.

5. Configure the `config.yaml` file:

   ```yaml
   kafka:
     bootstrap_servers: localhost:9092
     topic: stock_data

   aws:
     s3_bucket: <your-s3-bucket-name>
     region: <your-aws-region>
   ```

## Data Ingestion 📥

1. Start the data ingestion Kafka producer:

   ```
   python kafka_producer.py
   ```

   This script fetches real-time stock market data and publishes it to the Kafka topic.

## Data Processing and Analysis 📊

1. Launch an Amazon EC2 instance and SSH into it.

2. Install Spark:

   ```
   # Download Spark
   wget https://apache.claz.org/spark/spark-3.1.2/spark-3.1.2-bin-hadoop3.2.tgz

   # Extract Spark
   tar xvf spark-3.1.2-bin-hadoop3.2.tgz

   # Set environment variables
   export SPARK_HOME=/path/to/spark-3.1.2-bin-hadoop3.2
   export PATH=$PATH:$SPARK_HOME/bin
   ```

3. Submit the Spark job for data processing and analysis:

   ```
   spark-submit --packages org.apache.spark:spark-sql-kafka-0-10_2.12:3.1.2 data_processing.py
   ```

   This script consumes data from the Kafka topic, performs analysis.


1. **Data Collection** 📊: Real-time stock market data is collected using Kafka, a distributed streaming platform. Kafka allows for efficient and scalable data ingestion from multiple sources.

2. **Data Ingestion** 📥: A Python script is used to consume stock market data from Kafka topics. The data is then transformed into a suitable format for further processing.

3. **Data Transformation** 🔄: The transformed data is processed and analyzed using Python libraries and statistical techniques. This step involves exploring patterns, identifying trends, and generating meaningful insights from the stock market data.

4. **Data Storage** 💾: The analyzed data is stored in Amazon S3 buckets, a highly scalable and secure object storage service provided by Amazon Web Services. S3 buckets offer durability, availability, and easy accessibility for storing large volumes of data.

5. **Querying Data** 🗃️: Amazon Athena, an interactive query service, is used to query the stored data in S3 buckets. Athena allows for ad-hoc querying of data using standard SQL syntax without the need for complex ETL processes.


