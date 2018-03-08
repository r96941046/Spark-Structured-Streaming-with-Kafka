## HDP configuration
1. Enable Kafka service through Ambari interface
2. Note that sandbox Kafka broker default port is 6667 not 9092, referencing issue [Kafka on HDP 2.6,2 doesn't consume messages from console producer](https://community.hortonworks.com/questions/147344/kafka-on-hdp-262-doesnt-consume-messages-from-cons.html), and then restart the Kafka service
3. Need to forward port for kafka broker, referencing [SANDBOX PORT FORWARDING GUIDE](https://hortonworks.com/tutorial/sandbox-port-forwarding-guide/section/1/)
4. Create topic and validate kafka with console producer and consumer referencing [Validate Kafka](https://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.6.2/bk_command-line-installation/content/validate_kafka.html)
5. [Check Kafka data](https://stackoverflow.com/questions/17730905/is-there-a-way-to-delete-all-the-data-from-a-topic-or-delete-the-topic-before-ev)

### Python dependencies in producer script(using Anaconda)
`pip install tweepy kafka-python`
