# KafkaStreaming
Data Ingestion with Kafka and Kafka Streaming

## Stream Processing
* Stream Processing acts on potentially endless and constantly evolving immutable data contained in data streams.
* Once data have been placed in a data stream, they cannot be modified. We must place a new record in the stream to override the existing data.
* Finally, data in data streams is typically less than 1MB in size and the data volume may vary from a few records an hour to thousands of requests per second.

## Stream Processing Examples
### Log Analysis
One of the first places many companies use stream processing is in log analysis. Companies often run microservices that constantly produce logs that are full of information that can be mined for:

* User behavior patterns
* Failure prediction
* Debugging
These logs generate a tremendous amount of data on an ongoing basis, which can be difficult to then analyze. To solve this issue, each log produced by a microservice becomes an event in a data stream.
Companies then build programs that can analyze and join on the events in these data streams to find insights into the data.
![image](https://github.com/user-attachments/assets/96d7b9ff-cf1c-4a4e-966e-57ed36931423)

## Web Analytics
Modern web applications measure almost every action a user takes on their site, for example:

* button clicks
* Page load times
* Session duration
The volume of these actions can quickly overwhelm a traditional data store (any place you keep data). Ingesting and analyzing this data can be difficult and companies use stream processing to analyze the data as it is generated.

The benefits of this process are:
* it lessens the long-term processing burden for companies because of the smaller dataset
* provides real-time analysis instead of long-running bath analyses that may only be updated periodically

![image](https://github.com/user-attachments/assets/5061f6f9-f69b-44ad-9900-70c2db3a3e64)

### Real-Time Pricing
Ride-sharing applications are a great example of data streaming for real-time analysis. They use real-time pricing that adjusts with environmental factors and instantaneous demand.
![image](https://github.com/user-attachments/assets/e46d4582-ad02-4fba-9468-87cd3a328db3)

## Stream Processing Examples Recap
Stream Processing is a critical component in a number of familiar technology applications:

* Finding patterns and meaningful data in disparate log messages in a microservices architecture
* Tracking user engagement in real-time with streaming website analytics
* Real-time pricing in ride-sharing applications based on demand and environmental conditions
* Stock buying/selling based on price, news, and social media sentiment

## Log-Structured Storage
One of the key innovations over the past decade in computing has been the emergence of log-structured storage as a primary means of storing data.
### Log-structured streaming
* Log-structured streams build upon the concept of append-only logs. One of the hallmarks of log-structured storage systems is that at their core they utilize append-only logs.
* Common characteristics of all log-structured storage systems are that they simply append data to log files on disk.
* These log files may store data indefinitely, for a specific time period, or until a specific size is reached.
* There are typically many log files on disk, and these log files are merged and compacted occasionally.
* When a log file is merged it means that two or more log files are joined together into one log file.
* When a log file is compacted it means that data from one or more files is deleted. Deletion is typically determined by the age of a record. The oldest records are removed, while the newest stay.
* Examples of real world log-structured data stores: Apache HBase, Apache Cassandra, Apache Kafka

## Apache Kafka as a Stream Processing Tool
* Kafka is one of the most popular streaming data platforms in the industry today.
* Provides an easy-to-use message queue interface on top of its append-only log-structured storage medium
* Kafka is a log of events
* In Kafka, an event describes something that has occurred, as opposed to a request for an action to be performed
* Kafka is distributed by default
* Fault tolerant by design, meaning it is hard to lose data if a node is suddenly lost
* Kafka scales from 1 to thousands of nodes
* Kafka provides ordering guarantees for data stored within it, meaning that the order in which data is received is the order in which data will be produced to consumers
* Commonly used data store for popular streaming tools like Apache Spark, Flink, and Samza

## Kafka Architecture
* Kafka servers are referred to as brokers
* All of the brokers that work together are referred to as a cluster
* Clusters may consist of just one broker, or thousands of brokers
* Apache Zookeeper(opens in a new tab) is used by Kafka brokers to determine which broker is the leader of a given partition and topic
* Zookeeper keeps track of which brokers are part of the Kafka cluster
* Zookeeper stores configuration for topics and permissions (Access Control Lists - ACLs)
* ACLs are Permissions associated with an object. In Kafka, this typically refers to a user’s permissions with respect to production and consumption, and/or the topics themselves.
* Kafka nodes may gracefully join and leave the cluster
* Kafka runs on the Java Virtual Machine (JVM)

### Kafka Clustering - Key Points
* Kafka servers are referred to as brokers and organized into clusters.
* Kafka uses Apache Zookeeper to keep track of topic and ACL configuration, as well as determine leadership and cluster management.
* Usage of ZooKeeper means that Kafka brokers can typically seamlessly join and leave clusters, allowing Kafka to grow easily as its usage increases or decreases.

![image](https://github.com/user-attachments/assets/95420481-f692-40a4-9be3-e014406b79fb)

### Kafka Data Partitioning
![image](https://github.com/user-attachments/assets/486c2af5-7040-4296-846e-f3754ed4dbe2)

#### Message Ordering
Message ordering is only guaranteed within a partition in Kafka. If your topic has more than one partition, Kafka provides no guarantees that the messages will be consumed in the order they were produced. For many applications, this is an acceptable tradeoff for increasing the parallelism and speed of consumption. Your producer applications may still add metadata to the event header or message body itself to indicate ordering. However, this logic would belong to your application, and not Kafka itself. For example, you may place an increasing ID sequence in every message (eg 1, 2, 3, and so on) or a granular timestamp to indicate the order of a message.




