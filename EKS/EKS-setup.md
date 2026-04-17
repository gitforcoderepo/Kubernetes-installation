---

````markdown
# 🚀 EKS Cluster Setup using CLI

A complete step-by-step guide to create and manage an Amazon EKS cluster using CLI tools.

---

## 🧰 Prerequisites

Make sure you have:
- AWS Account ✅
- IAM user with required permissions 🔐
- Basic knowledge of Kubernetes ☸️

---

## ✅ Step 1: Install AWS CLI

```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
````

### 🔍 Verify:

```bash
aws --version
```

---

## ✅ Step 2: Configure AWS Credentials

```bash
aws configure
```

### Enter the following:

* Access Key
* Secret Key
* Region → `ap-south-1`
* Output format → `json`

---

## ✅ Step 3: Install eksctl

```bash
curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp

sudo mv /tmp/eksctl /usr/local/bin
```

### 🔍 Verify:

```bash
eksctl version
```

---

## ✅ Step 4: Install kubectl

```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"

chmod +x kubectl
sudo mv kubectl /usr/local/bin/
```

### 🔍 Verify:

```bash
kubectl version --client
```

---

## 🚀 Step 5: Create EKS Cluster

```bash
eksctl create cluster \
  --name my-cluster \
  --region ap-south-1 \
  --nodegroup-name my-nodes \
  --node-type t3.micro \
  --nodes 2
```

---

## ⏳ What Happens Behind the Scenes?

This command will automatically:

* 🏗 Create a VPC
* 🎯 Set up EKS Control Plane
* 💻 Launch EC2 Worker Nodes
* 🌐 Configure Networking

⏱ **Estimated Time:** 10–20 minutes

---

## ✅ Step 6: Verify Cluster

```bash
kubectl get nodes
```

### ✅ Expected Output:

```bash
NAME           STATUS   ROLES    AGE   VERSION
ip-xxxx        Ready    <none>   ...   ...
```

---

## ✅ Step 7: Test Deployment

```bash
kubectl create deployment nginx --image=nginx
kubectl expose deployment nginx --type=LoadBalancer --port=80
```

### Check Service:

```bash
kubectl get svc
```

🎯 **Note:**
This time, **EXTERNAL-IP will work** because EKS integrates with AWS Load Balancer.

---

# ⚠️ Important Tips

## 💸 Cost Warning

EKS is **NOT free**:

* Control plane ≈ $0.10/hour
* EC2 nodes cost extra

👉 Always delete cluster after use!

---

## 🔐 IAM Permissions Required

Ensure your AWS user/role has:

* EKS
* EC2
* CloudFormation
* IAM

---

## 🧹 Delete Cluster (VERY IMPORTANT)

```bash
eksctl delete cluster --name my-cluster --region ap-south-1
```

---

## ✅ 🔍 Verify Deletion

```bash
eksctl get cluster
```

✔ Should return **no clusters**
✔ Ensures no unwanted billing 💸

---

# 🎯 Summary

| Step | Action          |
| ---- | --------------- |
| 1    | Install AWS CLI |
| 2    | Configure AWS   |
| 3    | Install eksctl  |
| 4    | Install kubectl |
| 5    | Create cluster  |
| 6    | Verify nodes    |
| 7    | Deploy app      |
| 8    | Delete cluster  |

---

# 🚀 Pro Tip

```bash
eksctl delete cluster --name my-cluster --region ap-south-1
```

💡 “No delete → AWS bill will start!” 😄

```

- 🧑‍🏫 **Slide deck (PPT for teaching)**
```
