# Use Google Cloud CLI with a service account

Earlier today, I ran some test on Google Cloud using the CLI.

Here's some example using `gcloud` and `bq` authenticated with a service account.

```shell

# list existing credentials
gcloud auth list

# Activate a new service account using the credentials from the `my-project-99b6d0fbed58.json` file.
gcloud auth activate-service-account zmoog-sa@my-project.iam.gserviceaccount.com --key-file ~/my-project-99b6d0fbed58.json

# Set an existing service account as active.
gcloud config set account zmoog-sa@my-project.iam.gserviceaccount.com

# Run some command, for example using `bq` the BigQuery CLI tool.
bq ls --project_id my-project

# When you're done, you can clean everything up by revoking the service account 
# from your CLI.
gcloud auth revoke zmoog-sa@my-project.iam.gserviceaccount.com
```
