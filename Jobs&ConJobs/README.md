
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
Here i have setted the `completions=6` in the `spec` section of the job which will launch 6 jobs `sequentially`. 

## Execution: 

<p align="center">
  <img width="1000" height="550" src="https://github.com/amit17133129/images/blob/main/images/completions.gif?raw=true">
</p>

## Parallelism in Jobs:

By default, Job Pods do not run in parallel. The optional parallelism field specifies the maximum desired number of Pods a Job should run concurrently at any given time.

The actual number of Pods running in a steady state might be less than the parallelism value if the remaining work is less than the parallelism value. If you have also set completions, the actual number of Pods running in parallel does not exceed the number of remaining completions. A Job may throttle Pod creation in response to excessive Pod creation failure.

## Execution:

<p align="center">
  <img width="1000" height="550" src="https://github.com/amit17133129/images/blob/main/images/parallelism.gif?raw=true">
</p>

