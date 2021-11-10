
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

<p align="center">
  <img width="1000" height="550" src="https://github.com/amit17133129/images/blob/main/images/jobs.gif?raw=true">
</p>
