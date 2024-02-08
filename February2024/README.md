		February ’24


# 07 Feb

## Deleting formation

```kubectl delete formation <formation_id> -n <namespace>```
NB: If we target the formation, there is no need for namespaceTesting rotate-backups recipe

```i rc rotate-backups```

```i rs``` [shows which all recipes are completed]

after rotate backup completes, check the logs of etcd-mgmt container. As, code to display the things related to rotate-backups [such as retention period, no of backups prevailing retention period]
kubectl get <etcd-pod-name> -c mgmt



# 06 Feb

Todays Final Milvyas-formation-id : 8a42c750-da10-4e31-9bbe-8e2caf4e220d == errored as the operator changed.

Failing the recipe, in some cases
```i recipe-fail <— recipe_id —>```

##Get bucket details

Target the formation

```i f <—formation-id—>```

```kubectl get secret | grep $ID```

get the name with appended -bucket at the end.
	eg: ```ff453fb6-c71f-413c-96a9-79743675be96-bucket```

```kubectl get secret -o yaml <secret-name>```
	eg: ```kubectl get secret -o yaml ff453fb6-c71f-413c-96a9-79743675be96-bucket```

will get all the values base64 encoded.

## Restore

```i rc restore source_formation_id='ff453fb6-c71f-413c-96a9-79743675be96' backup_id='ff453fb6-c71f-413c-96a9-79743675be96' cos_bucket='ff453fb6-c71f-413c-96a9-79743675be96' cos_endpoint='s3.direct.eu.cloud-object-storage.appdomain.cloud' cos_region='eu-standard' cos_access_key='fd0121758cf8491cb07acc42d76dfd32' cos_secret_access_key='2c43a44c9ee72cfa001fd18a9561545c315ce1e80f6db331' name='ff453fb6-c71f-413c-96a9-79743675be96' restore_data='{"archive_name":"91853d6b-7cb2-4ed5-9a86-fa7626e62470.tar.gz","cos_key":"etcd_backup/account/66c8bc40f9b94f079bf179c863e51df8/formation/ff453fb6-c71f-413c-96a9-79743675be96/ff453fb6-c71f-413c-96a9-79743675be96.tar.gz"}'```


## DB Version Change

```i rc db-version-change version=1.1.2.0.99```

To find the milvus formation id from lh formation

```kubectl get formations -A -l cloudServiceInstanceId=8a446e60-b3ce-49c9-8210-73440868ee12```

Adding comments to the formation

```databases.cloud.ibm.com/note: '[2024-06-02] milvus test (Abhirami)'```


# 05 Feb

## Currents 

API-KEY : VB90RbsF-0t3g9N4V1n9LSfv9gHraNygpVBlwdZ5Pw-y
LH-FormationID:  

 
## Setting up from eu-de

* Create lakehouse formation on eu-de
* Target data plane <— fihjl —>
* Change operator in <— fihjl —> using kuebctl edit deploy operator -n compose-system
    * Get image from <— hdm_rakesh_milvus —>
* Now target control plane <— eex9w —> 
* Change dispatcher in <— eex9w —> 
    * Get image from <— milvus_ga —>
* Change middle-end 
    * Get image from <— scale abhirami —>

NB:	```kubectl edit cm compose-release -n compose-system```
	change the version according to the version


##Testing 

adding data to  milvus db

* To get the hostname:
	* i f <formation-id>
    * get hostname from connections tab:
           <-- method -->://<-- hostname -->:<-- portname -->
*  add the hostname in the following space in hello_milvus,py
```print(fmt.format("start connecting to Milvus"))```
```connections.connect(host="<host>", port="<grpc-port>", secure=True, server_name="localhost", user="ibmlhapikey", password="<ibm-apikey>")```
Run the following
```python3 hello-milvus.py```


## Editing CronJob

    - To list all the corncobs available
```kubectl get cronjob```
    - To start editing the formation.
```kubectl edit cronjob <— cronjob-name —>```

    - No go to spec>schedule in cronjob file.

    - Edit the schedule according to the UTC time.

Save[[esc]:wq]


Taking backup

The above edited cronjob will trigger at  the time specified in the cronjob





# 01 Feb


Lakehouse formation: 3502591a-603f-48c3-adc0-d962fd36f119 
Milvus: f358b247-15ba-43af-826b-4f5e9ef6e23e
		

* Don’t forget to change db-version of lakehouse before creating milvus formation



