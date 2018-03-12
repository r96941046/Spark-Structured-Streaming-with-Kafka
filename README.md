# Structured Streaming + Kafka

## Introduction

### [Kafka](https://kafka.apache.org/intro)

### [Spark Structured Streaming](https://spark.apache.org/docs/latest/structured-streaming-programming-guide.html)

_Structured Streaming provides fast, scalable, fault-tolerant, end-to-end exactly-once stream processing without the user having to reason about streaming._

1. Same expression as spark batch computation.
2. Spark DataFrame API in Scala, Java, Python or R, and is executed on the Spark SQL engine.
3. Ensuring end-to-end, exactly-once fault tolerance guarantee through checkpointing and Write Ahead Logs.
4. Micro-batch processing, and a new low-latency processing mode (as low as 1 millisecond) called Continuous Processing.
5. The key idea is to treat a live data stream as a table that is being continuously appended, and Spark runs computation as an incremental query on the unbounded input table.
6. Spark only keeps the minimal intermediate state data as required to update the result, and does not materialize the entire source table.

## Installation
Please follow the instructions below for Spark Structured Streaming + Kafka demo.

### Environment
1. Kafka consumer + Spark ([Hortonworks HDP 2.6 Sandbox VM](https://hortonworks.com/downloads/))
2. Local Kafka producer ([custom Python script](https://github.com/r96941046/Spark-Structured-Streaming-with-Kafka/blob/master/producer.py))

### HDP configuration
1. Enable Kafka service through Ambari interface
2. Note that sandbox Kafka broker default port is 6667 not 9092, referencing issue [Kafka on HDP 2.6,2 doesn't consume messages from console producer](https://community.hortonworks.com/questions/147344/kafka-on-hdp-262-doesnt-consume-messages-from-cons.html). If port is required to change, remember to change the port and then restart Kafka service
3. Need to forward HDP sandbox VM port for kafka broker, referencing [SANDBOX PORT FORWARDING GUIDE](https://hortonworks.com/tutorial/sandbox-port-forwarding-guide/section/1/)
4. Create topic and validate kafka with console producer and consumer referencing [Validate Kafka](https://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.6.2/bk_command-line-installation/content/validate_kafka.html)
5. [Where Kafka data is on HDP sandbox](https://stackoverflow.com/questions/17730905/is-there-a-way-to-delete-all-the-data-from-a-topic-or-delete-the-topic-before-ev)

### Pyspark configuration
Please follow [Pyspark Interpreter not working on Zeppelin](https://community.hortonworks.com/questions/176943/pyspark-interpreter-not-working-on-zeppelin.html) to solve Pyspark problem on HDP 2.6 Zeppelin.

### Spark Structured Streaming dependencies
Please add the library `org.apache.spark:spark-sql-kafka-0-10_2.11:2.2.0` to Zeppelin spark2 interpreter, referencing [Structured Streaming + Kafka Integration Guide (Kafka broker version 0.10.0 or higher)](https://spark.apache.org/docs/latest/structured-streaming-kafka-integration.html#deploying), and restart the interpreter. Library versions please see `Ambari>Admin>Stack and Versions`.

### Python dependencies in local producer script(using Anaconda)
Run the following command locally to install python dependencies
`pip install tweepy kafka-python`

### Start the producer locally to stream tweets to kafka in HDP sandbox
[Configure a twitter app](https://apps.twitter.com/) and put app information in [producer.py](https://github.com/r96941046/Spark-Structured-Streaming-with-Kafka/blob/master/producer.py). After that, run
`python producer.py`

### Import Zeppelin Notebook
In Zeppelin interface on HDP, please import [the notebook in this repo](https://raw.githubusercontent.com/r96941046/Spark-Structured-Streaming-with-Kafka/master/Spark%20Structured%20Streaming%20with%20Kafka.json) to see consumer in Spark Structured Streaming in action.

## References
1. [Structured Streaming Programming Guide](https://spark.apache.org/docs/latest/structured-streaming-programming-guide.html)
2. [Structured Streaming + Kafka Integration Guide ](https://spark.apache.org/docs/latest/structured-streaming-kafka-integration.html)
3. [kafka-python-client-example](http://www.biglittleant.cn/2016/12/28/kafka-python/)
4. [Pyspark: Parse a column of json strings](https://stackoverflow.com/questions/41107835/pyspark-parse-a-column-of-json-strings)
5. [Apache Spark Structured Streaming](https://jhui.github.io/2017/01/15/Apache-Spark-Streaming/)
6. [pyspark.sql module](http://spark.apache.org/docs/2.1.0/api/python/pyspark.sql.html)
7. [What Spark's Structured Streaming really means](https://www.infoworld.com/article/3052924/analytics/what-sparks-structured-streaming-really-means.html)
