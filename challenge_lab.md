# Perform Foundational Data, ML, and AI Tasks in Google Cloud: Challenge Lab

### set project

```
export MY_PROJECT='qwiklabs-gcp-00-64901e6177cd'
```


# Create a bigquery dataset called `lab_801`

### bq help methods

* `bq --help` command options
* `bq help` commands



```
export MY_DATASET='lab_819'
bq mk ${MY_DATASET}
```


# Create a Cloud Storage Bucket called `TBD`

### gsutil help mb

* `gsutil help mb` for make bucket commands

```
export MY_BUCKET='gs://86435c33-d0e1-4544-a072-e79898f653bf'
gsutil mb ${MY_BUCKET}
```

# command line for the job raw


```
export MY_BUCKET='gs://86435c33-d0e1-4544-a072-e79898f653bf'
export MY_PROJECT='qwiklabs-gcp-00-64901e6177cd'
export ID='882'
export MY_DATASET='lab_819'
gsutil mb ${MY_BUCKET}
bq mk ${MY_DATASET}
gcloud dataflow jobs run try2 --gcs-location gs://dataflow-templates-us-central1/latest/GCS_Text_to_BigQuery --region us-central1 --staging-location ${MY_BUCKET}/temp --parameters javascriptTextTransformGcsPath=gs://cloud-training/gsp323/lab.js,JSONPath=gs://cloud-training/gsp323/lab.schema,javascriptTextTransformFunctionName=transform,outputTable=${MY_PROJECT}:${MY_DATASET}.customers_${ID},inputFilePattern=gs://cloud-training/gsp323/lab.csv,bigQueryLoadingTemporaryDirectory=${MY_BUCKET}/bigquery_temp
```

# Dataproc

#### create cluster

```
gcloud dataproc clusters create cluster-8b05 --region us-east1 --zone us-east1-c --master-machine-type n1-standard-4 --master-boot-disk-size 500 --num-workers 2 --worker-machine-type n1-standard-4 --worker-boot-disk-size 500 --image-version 2.0-debian10 --project ${MY_PROJECT}
```

#### ssh to master node

```
hdfs dfs -cp gs://cloud-training/gsp323/data.txt /data.txt
```

### the job is not cli

```
POST /v1/projects/qwiklabs-gcp-00-64901e6177cd/regions/us-east1/jobs:submit/
{
  "projectId": "qwiklabs-gcp-00-64901e6177cd",
  "job": {
    "placement": {
      "clusterName": "cluster-8b05"
    },
    "statusHistory": [],
    "reference": {
      "jobId": "job-08eb4dc9",
      "projectId": "qwiklabs-gcp-00-64901e6177cd"
    },
    "scheduling": {
      "maxFailuresPerHour": "1"
    },
    "sparkJob": {
      "mainClass": "org.apache.spark.examples.SparkPageRank",
      "properties": {},
      "jarFileUris": [
        "file:///usr/lib/spark/examples/jars/spark-examples.jar"
      ],
      "args": [
        "/data.txt"
      ]
    }
  }
}
```

#### cli syntax

(docs)[https://cloud.google.com/sdk/gcloud/reference/dataproc/jobs/submit]

```

gcloud dataproc jobs submit spark --cluster my_cluster --jar my_jar.jar -- arg1 arg2

```




# Dataprep
click the pencil icon

click the column names and then filter rows




















# cloud speach

#### create api key

api and services
create credenditals
creat api key

export API_KEY=AIzaSyDMiAlz_UVcdSD69QHYpostwFfMk6waja0

```
{
  "config": {
      "encoding":"FLAC",
      "languageCode": "en-US"
  },
  "audio": {
      "uri":"gs://cloud-training/gsp323/task4.flac"
  }
}

curl -s -X POST -H "Content-Type: application/json" --data-binary @request.json "https://speech.googleapis.com/v1/speech:recognize?key=${API_KEY}" > task4-gcs-851.result

gsutil cp task4-gcs-851.result   gs://qwiklabs-gcp-00-64901e6177cd-marking/

```

