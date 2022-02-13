# Dataflow: Qwik Start - Python

# 

# IAM and Admin  

[200~Confirm that the default compute Service Account {project-number}-compute@developer.gserviceaccount.com is present and has the editor role assigned. The account prefix is the project number, which you can find on Navigation menu > Home.


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

# Create a Cloud Storage bucket

# Install pip and the Cloud Dataflow SDK

```
python3 --version
pip3 --version
sudo pip3 install -U pip
sudo pip3 install --upgrade virtualenv
virtualenv -p python3.7 env
source env/bin/activate
pip install apache-beam[gcp]
# it will auto replace the output file name
python -m apache_beam.examples.wordcount --output OUTPUT_FILE
```

You can now list the files that are on your local cloud environment to 
get the name of the OUTPUT_FILE:

```
ls
```

# Run an Example Pipeline Remotely

Set the BUCKET environment variable to the bucket you created earlier.

BUCKET=gs://<bucket name provided earlier>

Now you'll run the wordcount.py example remotely:

```
python -m apache_beam.examples.wordcount --project $DEVSHELL_PROJECT_ID \
  --runner DataflowRunner \
  --staging_location $BUCKET/staging \
  --temp_location $BUCKET/temp \
  --output $BUCKET/results/output \
  --region us-central1
```

 added to the role data flow service agent role in the initial service agent iam






























