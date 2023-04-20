# List resources using the CLI

Login using a service principal:

```shell
$ az login --tenant TENANT --service-principal -u CLIENT_ID -p CLIENT_SECRET
```

If you have multiple subscription, you can select one:

```shell
$ az account set --subscription SUBSCRIPTION_ID
```

And finally, we can list the resources of the `Microsoft.Storage/storageAccounts` type:

```shell
$ az resource list --resource-type "Microsoft.Storage/storageAccounts" 
```
