# Dataflow: Qwik Start - Templates

# 

In the Google Cloud console, on the Navigation menu (nav-menu.png), click IAM & Admin > IAM.

Confirm that the default compute Service Account {project-number}-compute@developer.gserviceaccount.com is present and has the editor role assigned. The account prefix is the project number, which you can find on Navigation menu > Home.

If the account is not present in IAM or does not have the editor role, follow the steps below to assign the required role.

In the Google Cloud console, on the Navigation menu, click Home.

Copy the project number (e.g. 729328892908).

On the Navigation menu, click IAM & Admin > IAM.

At the top of the IAM page, click Add.

For New principals, type:

{project-number}-compute@developer.gserviceaccount.com
Copied!
Replace {project-number} with your project number.

For Role, select Project (or Basic) > Editor. Click Save.

Ensure that the Dataflow API is successfully enabled
To ensure access to the necessary API, restart the connection to the Dataflow API.

In the Cloud Console, enter "Dataflow API" in the top search bar. Click on the result for Dataflow API.

Click Manage.

Click Disable API.

If asked to confirm, click Disable.

Click Enable.

# Create a Cloud BigQuery Dataset and Table Using Cloud Shell
Let's first create a BigQuery dataset and table.

Note: This section uses the bq command-line tool. Skip down if you want to run through this lab using the console.
Run the following command to create a dataset called taxirides:

bq mk taxirides
Copied!
Your output should look similar to:

Dataset '<myprojectid:taxirides>' successfully created

Now that you have your dataset created, you'll use it in the following step to instantiate a BigQuery table. Run the following command to do so:

bq mk \
--time_partitioning_field timestamp \
--schema ride_id:string,point_idx:integer,latitude:float,longitude:float,\
timestamp:timestamp,meter_reading:float,meter_increment:float,ride_status:string,\
passenger_count:integer -t taxirides.realtime
Copied!
Your output should look similar to:

Table 'myprojectid:taxirides.realtime' successfully created

On it's face, the bq mk command looks a bit complicated. However, with some assistance from the BigQuery command-line documentation, we can break down what's going on here. For example, the documentation tells us a little bit more about schema:

Either the path to a local JSON schema file or a comma-separated list of column definitions in the form [FIELD]:[DATA_TYPE], [FIELD]:[DATA_TYPE].
In this case, we are using the latter—a comma-separated list.

## Create a storage bucket
Now that we have our table instantiated, let's create a bucket. Run the following commands to do so:

export BUCKET_NAME=<your-unique-name>
Copied!
gsutil mb gs://$BUCKET_NAME/
Copie

## look at bigquery for this dataset
You should now see the taxirides dataset underneath your project ID in the left-hand console.

Click on the three dots next to taxirides dataset and select Open. Then select CREATE TABLE in the right-hand side of the console.

In the Destination > Table Name input, enter realtime.

Under Schema, toggle the Edit as text slider and enter the following:

```
ride_id:string,point_idx:integer,latitude:float,longitude:float,timestamp:timestamp,
meter_reading:float,meter_increment:float,ride_status:string,passenger_count:integer
```


## create a storage bucket

this is a dupe

# Run the Pipeline
From the Navigation menu find the Big Data section and click on Dataflow.

Click on + Create job from template at the top of the screen.

Enter iotflow as Job name for your Cloud Dataflow job.

Under Dataflow Template, select the Pub/Sub Topic to BigQuery template.

Under Input Pub/Sub topic, enter:

projects/pubsub-public-data/topics/taxirides-realtime
Copied!
Under BigQuery output table, enter the name of the table that was created:

<myprojectid>:taxirides.realtime
Copied!
Add your bucket as Temporary Location:

gs://Your_Bucket_Name/temp

# Run the Pipeline
From the Navigation menu find the Big Data section and click on Dataflow.

Click on + Create job from template at the top of the screen.

Enter iotflow as Job name for your Cloud Dataflow job.

Under Dataflow Template, select the Pub/Sub Topic to BigQuery template.

Under Input Pub/Sub topic, enter:

projects/pubsub-public-data/topics/taxirides-realtime
Copied!
Under BigQuery output table, enter the name of the table that was created:

<myprojectid>:taxirides.realtime
Copied!
Add your bucket as Temporary Location:

gs://Your_Bucket_Name/temp


