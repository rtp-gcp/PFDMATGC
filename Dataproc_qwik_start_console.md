# Dataproc Qwik Start Console

## Ensure API is enabled

Cloud Dataproc API

Create a cluster
In the Cloud Platform Console, select Navigation menu > Dataproc > Clusters, then click Create cluster.

Set the following fields for your cluster. Accept the default values for all other fields.

Field	Value
Name	example-cluster
Region	us-central1
Zone	us-central1-a

## submit a job

Set the following fields to update Job. Accept the default values for all other fields.

Field	Value
Cluster	example-cluster
Job type	Spark
Main class or jar	org.apache.spark.examples.SparkPi
Jar files	file:///usr/lib/spark/examples/jars/spark-examples.jar
Arguments	1000 (This sets the number of tasks.)

### equiv cmd line

```
gcloud dataproc jobs wait job-ee77dad9 --project qwiklabs-gcp-03-f29c70f988f3 --region us-central1
```



## update cluster

To change the number of worker instances in your cluster:

Select Clusters in the left navigation pane to return to the Dataproc Clusters view.
Click example-cluster in the Clusters list. By default, the page displays an overview of your cluster's CPU usage.
Click Configuration to display your cluster's current settings.
Configuration-details.png

Click Edit. The number of worker nodes is now editable.
Enter 4 in the Worker nodes field.
Click Save.
cluster-update.png


