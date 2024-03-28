# Rolling Updates and Rollback
  - Take me to [Video Tutorial](https://kodekloud.com/topic/rolling-updates-and-rollbacks/)
  
In this section, we will take a look at rolling updates and rollback in a deployment
Rolling Update Deployment. The rolling deployment is the default deployment strategy in Kubernetes. It replaces pods, one by one, of the previous version of our application with pods of the new version without any cluster downtime.
When using the RollingUpdate strategy, there are two more options that let us fine-tune the update process:

maxSurge: The number of pods that can be created above the desired amount of pods during an update. This can be an absolute number or percentage of the replicas count. The default is 25%.

maxUnavailable: The number of pods that can be unavailable during the update process. This can be an absolute number or a percentage of the replicas count; the default is 25%.

## Rollout and Versioning in a Deployment

  ![rollv](../../images/rollv.PNG)
  
## Rollout commands
- You can see the status of the rollout by the below command
  ```
  $ kubectl rollout status deployment/myapp-deployment
  ```
- To see the history and revisions
  ```
  $ kubectl rollout history deployment/myapp-deployment
  ```
 
  ![rollc](../../images/rollc.PNG)
  
## Deployment Strategies
- There are 2 types of deployment strategies
  1. Recreate
  2. RollingUpdate (Default Strategy)
  
  ![dst](../../images/dst.PNG)
  
## kubectl apply
- To update a deployment, edit the deployment and make necessary changes and save it. Then run the below command.
  ```
  apiVersion: apps/v1
  kind: Deployment
  metadata:
   name: myapp-deployment
   labels:
    app: nginx
  spec:
   template:
     metadata:
       name: myap-pod
       labels:
         app: myapp
         type: front-end
     spec:
      containers:
      - name: nginx-container
        image: nginx:1.7.1
   replicas: 3
   selector:
    matchLabels:
      type: front-end       
  ```
  ```
  $ kubectl apply -f deployment-definition.yaml
  ```
- Alternate way to update a deployment say for example for updating an image.
  ```
  $ kubectl set image deployment/myapp-deployment nginx=nginx:1.9.1
  ```
  ![ka](../../images/ka.PNG)
  
## Recreate vs RollingUpdate
  
  ![rcrl](../../images/rcrl.PNG)
  
## Upgrades

  ![up](../../images/up.PNG)
  
## Rollback
  
  ![rb](../../images/rb.PNG)
  
- To undo a change
  ```
  $ kubectl rollout undo deployment/myapp-deployment
  ```
  
## kubectl create
- To create a deployment
  ```
  $ kubectl create deployment nginx --image=nginx
  ```
## Summarize kubectl commands
```
$ kubectl create -f deployment-definition.yaml
$ kubectl get deployments
$ kubectl apply -f deployment-definition.yaml
$ kubectl set image deployment/myapp-deployment nginx=nginx:1.9.1
$ kubectl rollout status deployment/myapp-deployment
$ kubectl rollout history deployment/myapp-deployment
$ kubectl rollout undo deployment/myapp-deployment
```

![sum](../../images/sum.PNG)
 
#### K8s Reference Docs
- https://kubernetes.io/docs/concepts/workloads/controllers/deployment
- https://kubernetes.io/docs/tasks/run-application/run-stateless-application-deployment
