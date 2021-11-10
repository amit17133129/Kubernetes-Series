
<p align="center">
  <img width="1000" height="550" src="https://github.com/amit17133129/images/blob/main/images/jobs&cronjob_Image.png?raw=true">
</p>

# What is jobs?

A Job creates one or more Pods and will continue to retry execution of the Pods until a specified number of them successfully terminate. As pods successfully complete, the Job tracks the successful completions. When a specified number of successful completions is reached, the task (ie, Job) is complete. Deleting a Job will clean up the Pods it created. Suspending a Job will delete its active Pods until the Job is resumed again.

## Running a Job

First we will create a job using command line using 
```
# creating a job and saving into myjob.yaml file
kubectl create job myjob --image=centos:7 --dry-run -o yaml > myjob.yaml

```
After creating `myjob.yaml` you can launch the job using `kubectl create -f myjob.yaml`. You can find the detailed hand-on part in the below gif image.

## Execution: 

<p align="center">
  <img width="1000" height="550" src="https://github.com/amit17133129/images/blob/main/images/jobs.gif?raw=true">
</p>

## Completions in Jobs:

A Job is completed when a specific number of Pods terminate successfully. By default, a non-parallel Job with a single Pod completes as soon as the Pod terminates successfully.

If you have a parallel Job, you can set a completion count using the optional completions field. This field specifies how many Pods should terminate successfully before the Job is complete. The completions field accepts a non-zero, positive value.

As you can find that i have just created a simple job that will complete the work and create a new job if its failed by any reason. But it will create only one job. If you had a requirement then you can create multiple jobs using completions keyuword in `myjob.yaml` file. The completions will helps to launch as many jobs as we have requested. 

```
apiVersion: batch/v1
kind: Job
metadata:
  creationTimestamp: null
  name: myjob1
spec:
  completions: 6
  template:
    metadata:
```
Here i have set the `completions=6` in the `spec` section of the job which will launch 6 jobs `sequentially`. 

## Execution: 

<p align="center">
  <img width="1000" height="550" src="https://github.com/amit17133129/images/blob/main/images/completions.gif?raw=true">
</p>

## Parallelism in Jobs:

By default, Job Pods do not run in parallel. The optional parallelism field specifies the maximum desired number of Pods a Job should run concurrently at any given time.

The actual number of Pods running in a steady state might be less than the parallelism value if the remaining work is less than the parallelism value. If you have also set completions, the actual number of Pods running in parallel does not exceed the number of remaining completions. A Job may throttle Pod creation in response to excessive Pod creation failure.

```
apiVersion: batch/v1
kind: Job
metadata:
  creationTimestamp: null
  name: myjob1
spec:
  parallelism: 6
  template:
    metadata:
```

Here i have set the `parallelism=6` in the `spec` section of the job which will launch 6 jobs `parallely`. 

## Execution:

<p align="center">
  <img width="1000" height="550" src="https://github.com/amit17133129/images/blob/main/images/parallelism.gif?raw=true">
</p>

## BackOffLimit in Jobs:

When a job fails repeatedly, it will eventually reach the configured backoffLimit. Once this limit is reached, the job will no longer be retried. The actual cause of failure for the job may be available in the logs of its pods, or in other events related to the job failure. If you wish to have a job that will retry indefinitely, you can set the restartPolicy to OnFailure. This will ensure the job restarts when it fails, and the backoffLimit will never be reached, essentially creating a Job that retries until successful.

We need to add `backoffLimit` in myjob.yaml file in the spec section.

```
apiVersion: batch/v1
kind: Job
metadata:
  creationTimestamp: null
  name: myjob1
spec:
  backoffLimit: 4
  template:
    metadata:
    
```
As you see that i have set `backoffLimit` to 4. i.e., if the jobs fails more than 4 times then it will not launch 5th job. A demop you can see in the below gif.

## Execution:

<p align="center">
  <img width="1000" height="550" src="https://github.com/amit17133129/images/blob/main/images/backoffLimit.gif?raw=true">
</p>



# What is CronJobs?

CronJobs are meant for performing regular scheduled actions such as backups, report generation, and so on. Each of those tasks should be configured to recur indefinitely (for example: once a day / week / month); you can define the point in time within that interval when the job should start.

The job yaml file created using two ways.
1. You can create using command line.
2. You can edit the myjob.yaml file.

## Creating cronjob using command line.
```

kubecvtl create cronjob mycronjob --image=centos:7 --schedule='* * * * *' --dry-run -o yaml > mycronjob.yaml

```
## Creating cronjob by editing myjob.yaml file.
In the myjob.yaml file you have to edit the following things to create cronjob.
1. Change the Kind name from `Job` to `CronJob`.
2. Add a `jobTemplate` section in spec section.
3. 
```
spec:
  jobTemplate:         # changed
    metadata:
      creationTimestamp: null
      name: mycronjob
    spec:
      template:
        metadata:
          creationTimestamp: null
        spec:
          containers:
          - image: centos:7
            name: mycronjob
```
As cronjob meant for running a job on a schedule. So, we need to add a schedule in the spec section of the cronjob.

```
spec:
  schedule: "* * * * *"   #changed
  jobTemplate:         # changed
    metadata:
      creationTimestamp: null
      name: mycronjob
    spec:
```
## Execution:
A detaled demo you can find in the below gif image.

<p align="center">
  <img width="1000" height="550" src="https://github.com/amit17133129/images/blob/main/images/cronjob.gif?raw=true">
</p>

## Suspending CronJob:
