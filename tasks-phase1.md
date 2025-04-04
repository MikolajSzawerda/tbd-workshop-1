IMPORTANT ❗ ❗ ❗ Please remember to destroy all the resources after each work session. You can recreate infrastructure by creating new PR and merging it to master.
  
![img.png](doc/figures/destroy.png)

1. Authors:

   groupr nr: **z4**

   repo: (github)[https://github.com/MikolajSzawerda/tbd-workshop-1]

2. Follow all steps in README.md.

3. In boostrap/variables.tf add your emails to variable "budget_channels".

4. From avaialble Github Actions select and run destroy on main branch.
   
5. Create new git branch and:
    1. Modify tasks-phase1.md file.
    
    2. Create PR from this branch to **YOUR** master and merge it to make new release. 
    
    ***place the screenshot from GA after succesfull application of release***


6. Analyze terraform code. Play with terraform plan, terraform graph to investigate different modules.

    ***describe one selected module and put the output of terraform graph for this module here***
   
7. Reach YARN UI
   ```shell
   gcloud compute ssh tbd-cluster-m --project=tbd-2025l-318731 --zone=europe-west1-d -- -L 8088:localhost:8088
   ```
   ![yarn_ui_ss1](doc/yarn_ui_ss1.png)
   ![yarn_ui_ss2](doc/yarn_ui_ss2.png)

8. Draw an architecture diagram (e.g. in draw.io) that includes:
    1. VPC topology with service assignment to subnets
    2. Description of the components of service accounts
    3. List of buckets for disposal
    4. Description of network communication (ports, why it is necessary to specify the host for the driver) of Apache Spark running from Vertex AI Workbech
  
    ![architecture_diagram](doc/tbd-task-8.png)

9. Create a new PR and add costs by entering the expected consumption into Infracost
For all the resources of type: `google_artifact_registry`, `google_storage_bucket`, `google_service_networking_connection`
create a sample usage profiles and add it to the Infracost task in CI/CD pipeline. Usage file [example](https://github.com/infracost/infracost/blob/master/infracost-usage-example.yml) 
   ```yaml
   version: 0.1
    usage:
      google_artifact_registry.registry:
        storage_gb: 60

      google_storage_bucket.tbd_code_bucket:
        storage_gb: 200
        monthly_class_a_operations: 100
        monthly_class_b_operations: 300
        monthly_egress_data_gb: 70

      google_storage_bucket.tbd_data_bucket:
        storage_gb: 400
        monthly_class_a_operations: 100
        monthly_class_b_operations: 300
        monthly_egress_data_transfer_gb:
          same_continent: 90
          worldwide: 40
          asia: 20
          china: 0

      google_service_networking_connection.private_vpc_connection:
        monthly_data_processed_gb: 200

   ```

   ***place the screenshot from infracost output here***

10. Create a BigQuery dataset and an external table using SQL
    
    ***place the code and output here***
   
    ***why does ORC not require a table schema?***

11. Find and correct the error in spark-job.py
    **Cause**
    Incorrect name of the bucket in `spark-job.py`

    **How to find**
    Task with incorrect bucket name is failing. In task view there is log with the exact error:
    ![spark_failed.png](tasks-phase1/spark-failed.png)

    **How to fix**
    Change the name of the bucket to correct name, in our case `tbd-2025l-318731-data`

12. Add support for preemptible/spot instances in a Dataproc cluster

    ***place the link to the modified file and inserted terraform code***
    
    
