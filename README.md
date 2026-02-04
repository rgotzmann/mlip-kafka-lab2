Overview
In this hands-on lab, you will work with Apache Kafka, a distributed streaming platform for large-scale, real-time data, and you’ll gain exposure to Docker containers. You will:

Use Docker to pull and run a local Kafka instance.

Establish a secure connection to a Kafka broker.

Produce and consume messages using Python.

Explore Kafka command-line tools (e.g., kcat) for inspection and monitoring.

This lab prepares you for the upcoming group project on Kafka streams. The notebook KafkaDemo.ipynb provides a step-by-step guide for Python interactions.

Learning Objectives
By the end of this lab, you will be able to:

Explain topics and offsets, and describe how they enable message continuity after consumer disconnects.

Configure and run a Python producer and consumer against a Kafka broker.

Use kcat (or an equivalent CLI) to inspect, manage, and monitor topics and messages.

Deliverables
Connection Setup

If you deployed Kafka on a remote server, cloud cluster, or a managed service, provide evidence of a secure SSH tunnel (command used, brief explanation, and a screenshot of an active tunnel).

Python Producer & Consumer

Implement producer and consumer modes by modifying the provided starter code.

Include:

The final Python scripts/notebook cells.

Sample output showing successful message production and consumption (with offsets).

kcat (or CLI) Demonstration

Show basic topic/message management and monitoring using kcat (or an approved alternative).

Include commands executed and screenshots or captured output (e.g., create/list/describe topic, read messages from beginning).

Getting Started
1) Clone the Starter Repository
Clone the starter code from this Git repository. (link unchanged)

The repository includes a Python notebook demonstrating Kafka producer and consumer patterns.

Note: If you encounter issues with kafka-python, uninstall it and install kafka-python-ng:

pip uninstall -y kafka-python
pip install kafka-python-ng

2) Environment & Dependencies
Use Python 3.9+ (recommended).

Create/activate a virtual environment (optional but recommended).

Install dependencies from requirements.txt:

pip install -r requirements.txt
Connecting to a remote Kafka Server (SSH Tunnel) - Not needed if you create your local containerized Kafka broker
Use SSH to create a local tunnel to the remote Kafka broker (find remote_server, user, and password on the Canvas entry for this lab):

ssh -L <local_port>:localhost:<remote_port> <user>@<remote_server> -NTf
Replace placeholders with the provided values.

Keep the tunnel open while running your producer/consumer locally.

Test that the broker is reachable (e.g., with kcat -L, see below).

 

Implementing Producer–Consumer Mode
Follow the TODO blocks in the starter scripts/notebook.

A) Producer Mode — Write Data to the Broker
Set bootstrap servers (e.g., localhost:<local_port> if tunneling).

Add 2–3 cities of your choice to publish as messages.

Run the code to produce messages to your Kafka topic.

Ref :

KafkaProducer DocumentationLinks to an external site.

B) Consumer Mode — Read Data from the Broker
Fill the TODO for the consumer configuration/arguments (topic, bootstrap servers, group id, etc.).

Run the consumer and verify output in Kafka_log.csv (as indicated in the starter).

 

Ref:

KafkaConsumer DocumentationLinks to an external site.

 

Concepts to be researched and explained:

Topic: Named stream of records, split into partitions.

Offset: Monotonically increasing position within a partition.

Continuity: Consumers track committed offsets; after a disconnect/restart, the consumer resumes from the last committed offset, avoiding duplicates (unless configured otherwise).

 

Using Kafka’s CLI Tools
kcat (formerly kafkacat)
Install:

macOS: brew install kcat

Ubuntu: apt-get install kcat

Windows note: Setting up kcat on Windows is non-trivial. For this deliverable, work in pairs with someone on macOS/Ubuntu during recitation. The goal is to understand CLI usage for the group project (Linux VMs).

Task: Using the kcat documentation, write a command that connects to your (tunneled) local broker, selects your topic, and consumes from the earliest offset.

Example (fill in your topic):

kcat -b localhost:<local_port> -t <your_topic> -C -o beginning -q
Other useful commands:

List metadata & topics:

kcat -b localhost:<local_port> -L
Produce a few test messages from stdin (quick sanity check):

seq 1 5 | kcat -b localhost:<local_port> -t <your_topic>
 

Ref:

kcat usageLinks to an external site.

kcat GitHubLinks to an external site.

 

Optional but Recommended
For your group project you’ll read movie data from Kafka. Try:

Listing all topics:

kcat -b localhost:9092 -L
If a movielog topic exists on your environment, consume a few messages to inspect the schema and typical fields.

 

Validation & Tips
Broker reachable? kcat -b localhost:<local_port> -L should display metadata.

Producer working? After running your producer code, consume with kcat from -o beginning to see your messages.

Consumer continuity? Start consumer → read some messages → stop → produce more → restart consumer and observe it continue from the next offset.

 

Troubleshooting
Connection refused/timeouts: Confirm SSH tunnel is active and ports match your client config.

Auth or version mismatch: Ensure client/broker compatibility and correct security settings if your environment requires them.

Empty consumption: Check the topic name, partition count, and whether you’re reading from -o beginning vs. the end.

Windows CLI issues: Use a Linux/macOS host or pair up during recitation for the kcat portion.

 

Additional Resources
Apache KafkaLinks to an external site.
Kafka for BeginnersLinks to an external site.
What is Apache Kafka? - TIBCOLinks to an external site.
Kafka Introduction Video 1Links to an external site.

 <- Recommended video for a quick 5-min introduction to Kafka
Kafka Introduction Video 2Links to an external site.

Docker Installation and Local Kafka.pdf

