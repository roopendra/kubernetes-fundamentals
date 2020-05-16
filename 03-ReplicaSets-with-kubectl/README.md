# Kubernetes - ReplicaSets

## Step-01: Introduction to ReplicaSets
- What are ReplicaSets?
- What is the advantage of using ReplicaSets?

## Step-02: ReplicaSets Demo

### Create ReplicaSet
- Create ReplicaSet
```
kubectl create -f replicaset-demo.yml
```
- **replicaset-demo.yml**
```yml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: my-nginx-rs
  labels:
    app: my-nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-nginx
  template:
    metadata:
      labels:
        app: my-nginx
    spec:
      containers:
      - name: my-first-nginx
        image: stacksimplify/kubenginx:1.0.0
```

### List ReplicaSets
- Get list of ReplicaSets
```
kubectl get rs
```

### Describe ReplicaSet
- Describe the newly created ReplicaSet
```
kubectl describe rs/<replicaset-name>
kubectl describe rs/my-first-nginx-rs
```

### List of Pods
- Get list of Pods
```
#Get list of Pods
kubectl get pods

# Get list of Pods with Pod IP and Node in which it is running
kubectl get pods -o wide
```

### Verify the Owner of the Pod
- Verify the owner reference of the pod.
```
kubectl get pods <Pod-name> -o yaml
kubectl get pods my-first-nginx-rs-449xd -o yaml
```

### Reliability or High Availability 
- Test how the high availability or reliability concept is achieved automatically in Kubernetes
- Whenever a POD is accidentally terminated due to some application issue, ReplicaSet should auto-create that Pod to maintain desired number of Replicas configured to achive High Availability.
```
# To get Pod Name
kubectl get pods

# Delete the Pod
kubectl delete pod <Pod-Name>

# Verify the new pod got created automatically
kubectl get pods   (Verify Age and name of new pod)
``` 

### Scalability
- Test how scalability is going to seamless & quick
- Update the **replicas** field in **replicaset-demo.yml** from 3 to 6.
```
# Before change
spec:
  replicas: 3

# After change
spec:
  replicas: 6
```
- Update the ReplicaSet
```
# Apply latest changes to ReplicaSet
kubectl replace -f replicaset-demo.yml

# Verify if new pods got created
kubectl get pods -o wide
```

### Delete ReplicaSet
```
# Delete ReplicaSet
kubectl delete rs/my-first-nginx-rs

# Verify if ReplicaSet got deleted
kubectl get rs
```

## Pending Concept in ReplicaSet
- We didn't discuss about **Labels & Selectors**
- This concept we can understand in detail when we are learning to write Kubernetes YAML manifest. 
- So we will understand about this during the **ReplicaSets-YAML** section.
