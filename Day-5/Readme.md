
---

###  Identify the Problems with the Containers

#### 1. **Scalability Limitations**
- **Lack of Auto-Scaling Support**: Containers do not automatically scale up or down based on application load.
  - **Scale-Up Requirement**:
    - When traffic increases, we need to manually add more containers or scale resources.
    - Options include:
      - **Vertical Scaling**: Manually increase CPU/RAM of the host system.
      - **Horizontal Scaling**: Add more containers or nodes to the cluster.
  - **Scale-Down Requirement**:
    - During low traffic, we need to manually remove containers or reduce system resources to optimize cost.

#### 2. **Lack of Built-in Load Balancing**
- Containers do not provide automatic traffic distribution between instances.
- Without a load balancer, incoming requests can overload certain containers while others remain underutilized.

#### 3. **No Fault Tolerance**
- **Single Point of Failure**: If a container crashes or stops, the application becomes unavailable unless manually restarted.
- Downtime can affect service availability and user experience.

#### 4. **No Self-Healing Mechanism**
- Containers do not auto-recover from failures.
- Manual intervention is required to restart or replace failed containers, leading to increased maintenance overhead.

---

### Solution: Use Container Orchestration Tools

To overcome the limitations of standalone containers, we use orchestration platforms like **Kubernetes**.

---

## Kubernetes Overview

- **Definition**: Kubernetes is an open-source **container orchestration** platform used for automating deployment, scaling, and management of containerized applications.
- **Function**: It manages container lifecycles, handles networking, performs auto-scaling, ensures high availability, and provides fault tolerance.

---

### Key Features of Kubernetes

1. **Orchestration** – Manages container deployment, updates, and lifecycle across nodes.
2. **Auto Scaling** – Dynamically adjusts the number of container instances based on traffic/load.
3. **Load Balancing** – Distributes network traffic evenly to avoid overload and ensure performance.
4. **Self-Healing** – Automatically restarts failed containers and reschedules on healthy nodes.
5. **Platform Independence** – Can run on any cloud or on-premises infrastructure.

---

### Kubernetes Setup and Cluster Creation (AWS EKS)

#### Prerequisites
- Jump Server/Bastion Host
- Tools to install:
  - `kubectl` – Kubernetes CLI
  - `eksctl` – EKS cluster provisioning tool
  - `awscli` – AWS command line interface

#### Steps to Create a Cluster
```bash
vi cluster.sh
chmod 777 cluster.sh
sh cluster.sh
aws configure

eksctl create cluster \
  --name vaishakh-cluster \
  --version 1.31 \
  --region eu-north-1 \
  --nodegroup-name test-linux \
  --node-type t3.micro \
  --nodes 3 \
  --nodes-min 3 \
  --nodes-max 5 \
  --managed

kubectl get nodes
```

---

### Deploying Applications in Kubernetes

1. Clone Manifest Repositories:
```bash
git clone https://github.com/Vaishakharekere/vaishakh-k8s-manifests.git
cd vaishakh-k8s-manifests
kubectl apply -f pod.yaml
kubectl get pods -o wide
kubectl describe pod sample-pod
```

2. Deploy Retail App:
```bash
git clone -b master https://github.com/Vaishakharekere/Retail-App_kubernetes.git
cd Retail-App_kubernetes
kubectl apply -f userprofile-deployment.yml
kubectl apply -f usernode-js-service.yml
kubectl get deployments
kubectl get svc
```

---

### Kubernetes Cluster Architecture

#### What is a Cluster?
- A group of **nodes** (machines) managed by Kubernetes.
- Includes:
  - **Master Node** (Control Plane)
  - **Worker Nodes** (Run the application)

---

#### Master Node Components:
1. **API Server** – Handles all requests and is the communication gateway for the cluster.
2. **ETCD** – A distributed key-value store for all cluster data.
3. **Controller Manager** – Ensures desired state of applications is maintained.
4. **Scheduler** – Assigns pods to available worker nodes based on resource availability.

---

#### Worker Node Components:
1. **Kubelet** – Agent that runs on each node, communicates with the master, and manages pod execution.
2. **Container Runtime** – Pulls container images, creates, starts, and manages containers (e.g., Docker, containerd).
3. **Kube-Proxy** – Manages network routing and load balancing between services and pods.

---

#### Pod
- The **smallest deployable unit** in Kubernetes.
- A pod encapsulates one or more containers, storage, and network configurations.
- Pods run on worker nodes and are scheduled by the master node.

---
