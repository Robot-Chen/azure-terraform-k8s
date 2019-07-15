# azure-terraform-k8s
create a k8s cluster in azure using terraform


### step 1 : create a container in your Azure storage account 

- All services / Storage accounts / 

```
az storage container create -n tfstate \
--account-name <YourAzureStorageAccountName> \
--account-key <YourAzureStorageAccountKey>
```

### step 2 : terraform init


```
terraform init \
-backend-config="storage_account_name=<YourAzureStorageAccountName>" \
-backend-config="container_name=tfstate" \
-backend-config="access_key=<YourStorageAccountAccessKey>" \
-backend-config="key=codelab.microsoft.tfstate"
```


### step 3 : get and expoort your appId and password

```
az ad sp create-for-rbac
```
- Replace the <your-client-id> and <your-client-secret> placeholders with the appId and password values

```
export TF_VAR_client_id=<your-client-id>
export TF_VAR_client_secret=<your-client-secret>
```
### step 4 : terraform plan


```
terraform plan -out out.plan

```

### step 5 : terraform apply

```
terraform apply out.plan

```
