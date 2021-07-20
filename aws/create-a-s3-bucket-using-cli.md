# Create a S3 bucket using CLI

According to the [AWS CLI Command Reference](https://docs.aws.amazon.com/cli/latest/reference/s3api/create-bucket.html):

> Regions outside of us-east-1 require the appropriate LocationConstraint to be specified in order to create the bucket in the desired region

So, to create my new shiny S3 bucket in the `eu-west-1` (Ireland) region I need the following command:

```shell
$ aws s3api create-bucket --bucket zmoog-stonky --region eu-west-1 --create-bucket-configuration LocationConstraint=eu-west-1
```
