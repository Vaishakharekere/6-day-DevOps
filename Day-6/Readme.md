
## Namespace:
Dividing a cluster into isolated environments.  
When we have multiple clusters, we use the concept of namespaces.

### Commands:
```bash
kubectl get namespace  
kubectl get all -n kube-system  

kubectl create ns vaishakh-ns  

kubectl get pods -n vaishakh-ns  
git pull  
kubectl apply -f rs.yaml  
kubectl get pods  
kubectl get pods -o wide  
kubectl get pods -n vaishakh-ns  
kubectl get rs -n vaishakh-ns  
kubectl get pods -n vaishakh-ns  
kubectl get pods -n vaishakh-ns  
```

---

## Deployment.yaml

### Types of Namespaces:
- **Default Namespace**: Created automatically by Kubernetes to create resources.  
- **kube-node-lease**: Used to check the health of nodes; Kubernetes master node uses Lease objects.  
- **kube-public**: Anyone can access resources in this namespace.  
- **kube-system**: During cluster creation, by default, all resources like metric server, CNI, CoreDNS, etc., are created in this namespace.

> **Note**: When deploying applications to production servers, we **should never** deploy applications in the default namespace.

---

### Creating a Custom Namespace:
```bash
kubectl create ns vaishakh-ns
```

---

### Delete a Pod:
```bash
kubectl delete pod test-pod -n vaishakh-ns
```

If the pod goes down, we face 3 major problems:

1. **Application Downtime** – To overcome this, we must attach **controllers** to the pod.  
2. **IP Address Changes** – Each pod has its own IP address. If the pod goes down, its IP changes. To solve this, create a **Service (static URL)** in Kubernetes.  
3. **Data Loss** – If the pod goes down, we may lose data. To prevent this, we must implement **Volumes** in Kubernetes.

---

## Replica Set:
- ReplicaSet is a Kubernetes object that maintains a **minimum number of pods** running **24/7**.  
- It always ensures **desired state = actual state**.

---

### Replica Set Problems:
In real-time applications, **we don’t recommend using ReplicaSet alone**, because it doesn’t support **rollout** or **rollback** operations.

---

## What is Deployment?
- In Kubernetes, we deploy applications using the **Deployment Controller**.
- It manages the ReplicaSet, and the ReplicaSet manages the Pods.

---

### Exposing Applications:
If we want to expose an application through a web browser, Kubernetes introduces an object called **Service**.

---

### Types of Services:
1. **ClusterIP Service**  
2. **NodePort Service**  
3. **LoadBalancer Service**

> **Implement LoadBalancer Service**

---

## Monitoring

To understand what’s happening inside the application, we implement **monitoring dashboards**.  
Monitoring helps us:
- Identify when something goes wrong.
- Analyze CPU/memory usage.
- Check the health of pods, nodes, and the overall cluster.

---

### Tools:
- **Prometheus**  
- **Grafana**

---

### Prometheus:
- Prometheus is a **metrics server** that collects **time-series data (TSDB)**.  
- It sends this data to the Grafana dashboard.

---

### Grafana:
- With Grafana, we set up **monitoring dashboards**.
- Data is visualized using **pie charts**, **graphs**, etc.

---

### Installation:
```bash
snap install helm --classic  
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts  
helm repo add grafana https://grafana.github.io/helm-charts  
```

---

## Ports:
- Prometheus: **9090**  
- Grafana: **80**

---

## Ansible:
- Ansible is a **configuration management tool** used for automation.

---

### Additional Commands:
```bash
kubectl cluster-info    # To get cluster info  
cd /root/.kube  
vi config
```

---

