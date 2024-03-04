# Taints and Tolerations
  - Take me to [Video Tutorial](https://kodekloud.com/topic/taints-and-tolerations-2/)
  
In this section, we will take a look at taints and tolerations.
- Pod to node relationship and how you can restrict what pods are placed on what nodes.

#### Taints and Tolerations are used to set restrictions on what pods can be scheduled on a node. 
- Only pods which are tolerant to the particular taint on a node will get scheduled on that node.

  ![tandt](../../images/tandt.PNG)
  
## Taints
- Use **`kubectl taint nodes`** command to taint a node.

  Syntax
  ```
  $ kubectl taint nodes <node-name> key=value:taint-effect
  ```
 
  Example
  ```
  $ kubectl taint nodes node1 app=blue:NoSchedule
  ```
  
- The taint effect defines what would happen to the pods if they do not tolerate the taint.
- There are 3 taint effects
  - **`NoSchedule`**
  - **`PreferNoSchedule`**
  - **`NoExecute`**
 
  - Taint effects define what will happen to pods if they don’t tolerate the taints. The three taint effects are:
  - NoSchedule: A strong effect where the system lets the pods already scheduled in the nodes run, but enforces taints from the subsequent pods.
  - PreferNoSchedule: A soft effect where the system will try to avoid placing a pod that does not tolerate the taint on the node.
  - NoExecute: A strong effect where all previously scheduled pods are evicted, and new pods that don’t tolerate the taint will not be scheduled.
  
  ![tn](../../images/tn.PNG)
  
## Tolerations
   - Tolerations are added to pods by adding a **`tolerations`** section in pod definition.
     ```
     apiVersion: v1
     kind: Pod
     metadata:
      name: myapp-pod
     spec:
      containers:
      - name: nginx-container
        image: nginx
      tolerations:
      - key: "app"
        operator: "Equal"
        value: "blue"
        effect: "NoSchedule"
     ```
    
  ![tp](../../images/tp.PNG)
    

#### Taints and Tolerations do not tell the pod to go to a particular node. Instead, they tell the node to only accept pods with certain tolerations.
- To see this taint, run the below command
  ```
  $ kubectl describe node kubemaster |grep Taint
  ```
 
 ![tntm](../../images/tntm.PNG)
  
     
#### K8s Reference Docs
- https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/

