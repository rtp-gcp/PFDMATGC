# Dataproc: Qwik Start - Command Line

Apache Spark
Apache Hadoop


```
Confirm that the default compute Service Account {project-number}-compute@developer.gserviceaccount.com is present and has the editor role assigned. The account prefix is the project number, which you can find on Navigation menu > Home.
```

gcloud config set dataproc/region us-central1

gcloud dataproc clusters create example-cluster --worker-boot-disk-size 500

gcloud dataproc jobs submit spark --cluster example-cluster \
  --class org.apache.spark.examples.SparkPi \
  --jars file:///usr/lib/spark/examples/jars/spark-examples.jar -- 1000

update a cluster ot be bigger

gcloud dataproc clusters update example-cluster --num-workers 4

gcloud dataproc clusters update example-cluster --num-workers 2

