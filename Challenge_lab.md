# Perform Foundational Data, ML, and AI Tasks in Google Cloud: Challenge Lab

### set project

# Create a bigquery dataset called `TBD`

### bq help methods

* `bq --help` command options
* `bq help` commands

# Create a Cloud Storage Bucket called `TBD`

### gsutil help mb

* `gsutil help mb` for make bucket commands


# command line for the job raw

Find the `ID`s in the variable big query table name.

```
export MY_BUCKET='gs://5e3ef5e9-f845-40ee-9ef0-4dd7fc2eb587'
export MY_PROJECT='qwiklabs-gcp-02-97d715b0c88b'
export LAB_ID='874'
export CUST_ID='400'
export MY_DATASET='lab_'${LAB_ID}
gsutil mb ${MY_BUCKET}
bq mk ${MY_DATASET}
```

```
gcloud dataflow jobs run try2 \
--gcs-location gs://dataflow-templates-us-central1/latest/GCS_Text_to_BigQuery \
--region us-central1 \
--staging-location ${MY_BUCKET}/temp \
--parameters javascriptTextTransformGcsPath=gs://cloud-training/gsp323/lab.js,\
JSONPath=gs://cloud-training/gsp323/lab.schema,\
javascriptTextTransformFunctionName=transform,\
outputTable=${MY_PROJECT}:${MY_DATASET}.customers_${CUST_ID},\
inputFilePattern=gs://cloud-training/gsp323/lab.csv,\
bigQueryLoadingTemporaryDirectory=${MY_BUCKET}/bigquery_temp
```

# Dataproc

#### create cluster

```
export MY_REGION=us-central1
```


```
gcloud dataproc clusters create cluster-8b05 --region ${MY_REGION} --zone ${MY_REGION}-c --master-machine-type n1-standard-4 --master-boot-disk-size 500 --num-workers 2 --worker-machine-type n1-standard-4 --worker-boot-disk-size 500 --image-version 2.0-debian10 --project ${MY_PROJECT}
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















# TASK 4

This is the video the support folks give

https://drive.google.com/file/d/19FLkfk5eN5Tx-xD5CTNId_Dzlwu2fhlU/view

time stamp 39:57 is where it starts lab 4

```
gcloud iam service-accounts create my-nalang-sa --display-name "my natural lang servcie account"

gcloud iam service-accounts keys create ~/key.json --iam-account my-nalang-sa@${GOOGLE_CLOUD_PROJECT}.iam.gserviceaccount.com

export GOOGLE_APPLICATION_CREDENTIALS="/home/${USER}/key.json"


gcloud auth activate-service-account my-nalang-sa@${GOOGLE_CLOUD_PROJECT}.iam.gserviceaccount.com --key-file=${GOOGLE_APPLICATION_CREDENTIALS}








## cloud speach

#### create api key

api and services
create credenditals
creat api key

```
export API_KEY='AIzaSyAxhsbhdBO9cEeGzRxfiBwdLVoLm0a-_68'
```

contents of request.json
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
```

Specify the variable part

```
export TASK4_NUM0='03'
export TASK4_NUM1='7ac715b9aee0'
export TASK4_NUM2='890'
export TASK4_NUM3='937'
```

```
curl -s -X POST -H "Content-Type: application/json" --data-binary @request.json "https://speech.googleapis.com/v1/speech:recognize?key=${API_KEY}" > task4-gcs-${TASK4_NUM2}.result

gsutil cp task4-gcs-${TASK4_NUM2}.result   gs://qwiklabs-gcp-${TASK4_NUM0}-${TASK4_NUM1}-marking/

```



## Natural Language Task

```
export GOOGLE_CLOUD_PROJECT=$(gcloud config get-value core/project)
gcloud iam service-accounts create my-natlang-sa   --display-name "my natural language service account"
gcloud iam service-accounts keys create ~/key.json   --iam-account my-natlang-sa@${GOOGLE_CLOUD_PROJECT}.iam.gserviceaccount.com
```

Need to update based upon the userid
```
export GOOGLE_APPLICATION_CREDENTIALS="/home/${USER}/key.json"
```

```
gcloud ml language analyze-entities --content="Old Norse texts portray Odin as one-eyed and long-bearded, frequently wielding a spear named Gungnir and wearing a cloak and a broad hat." > task4-cnl-${TASK4_NUM3}.result
```

```
gsutil cp task4-cnl-${TASK4_NUM3}.result gs://qwiklabs-gcp-00-${TASK4_NUM1}-marking/
```

## Video Analysis Task



SEtup authoorization

gcloud iam service-accounts create quickstart

gcloud iam service-accounts keys create key.json --iam-account quickstart@<your-project-123>.iam.gserviceaccount.com

gcloud iam service-accounts keys create key.json --iam-account quickstart@qwiklabs-gcp-04-c4b2502664ad.iam.gserviceaccount.com


gcloud auth activate-service-account --key-file key.json

gcloud auth print-access-token

cat > request.json <<EOF
{
   "inputUri":"gs://spls/gsp154/video/train.mp4",
   "features": [
       "LABEL_DETECTION"
   ]
}
EOF

curl -s -H 'Content-Type: application/json' \
    -H 'Authorization: Bearer '$(gcloud auth print-access-token)'' \
    'https://videointelligence.googleapis.com/v1/videos:annotate' \
    -d @request.json



Use the result for this, replace operations, projects and region

curl -s -H 'Content-Type: application/json' \
    -H 'Authorization: Bearer '$(gcloud auth print-access-token)'' \
    'https://videointelligence.googleapis.com/v1/projects/PROJECTS/locations/LOCATIONS/operations/OPERATION_NAME'

curl -s -H 'Content-Type: application/json' \
    -H 'Authorization: Bearer '$(gcloud auth print-access-token)'' \
    'https://videointelligence.googleapis.com/v1/projects/757365958302/locations/us-east1/operations/10848866320574601713'

## This worked

```
gcloud iam service-accounts create my-natlang-sa   --display-name "my natural language service account"
gcloud iam service-accounts keys create ~/key.json   --iam-account my-natlang-sa@${GOOGLE_CLOUD_PROJECT}.iam.gserviceaccount.com
export GOOGLE_APPLICATION_CREDENTIALS="/home/$USER/key.json"
gcloud auth activate-service-account my-natlang-sa@${GOOGLE_CLOUD_PROJECT}.iam.gserviceaccount.com --key-file=$GOOGLE_APPLICATION_CREDENTIALS
gcloud ml language analyze-entities --content="Old Norse texts portray Odin as one-eyed and long-bearded, frequently wielding a spear named Gungnir and wearing a cloak and a broad hat." > result.json
gcloud auth login
gsutil cp result.json gs://qwiklabs-gcp-02-97d715b0c88b-marking/task4-cnl-927.result
```

