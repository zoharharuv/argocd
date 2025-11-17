Here is the **complete README.md file**, ready to paste directly into your GitHub repo:

---

# ArgoCD + Helm Deployment on OpenShift

### Training Project – Red Hat OpenShift & GitOps Workshop

This repository contains a sample application deployed using **Helm**, **ArgoCD**, and **OpenShift** as part of the Red Hat OpenShift & GitOps training course.

The goal of this project is to demonstrate:

* How to deploy applications using **GitOps**
* How to template Kubernetes manifests using **Helm**
* How ArgoCD continuously syncs applications from Git
* How OpenShift resources (Routes, DeploymentConfigs, RBAC, etc.) integrate into the workflow

---

## 📁 Project Structure

```
argocd/
├── Application/          # ArgoCD Application manifest
├── charts/               # Helm chart directory
│   ├── templates/        # Kubernetes manifests (Deployment, Service, Route, ConfigMap)
│   ├── Chart.yaml        # Chart metadata
│   └── values.yaml       # Default values
└── README.md             # Documentation
```

---

## 🚀 What This Project Demonstrates

### ✔ **Full GitOps Flow**

ArgoCD tracks this Git repository and automatically:

* Detects changes
* Compares live vs desired state
* Applies updates to the cluster
* Highlights drift (OutOfSync)

### ✔ **Helm Chart Templating**

Using `.Values` and `.Chart` you can dynamically configure:

* container image & tag
* port
* replica count
* ConfigMap content
* route name
* health checks

### ✔ **OpenShift Native Features**

This project uses:

* **Route** (OpenShift’s native ingress resource)
* **SecurityContext defaults**
* **Health probes** for liveliness & readiness
* **ConfigMap volume mounts**

---

## 🔧 Deployment Instructions

### **1. Login to OpenShift**

```bash
oc login --token=<token> --server=<openshift-api-url>
```

### **2. Create the ArgoCD Application**

You can apply it manually:

```bash
oc apply -f Application/application.yaml
```

Or create it via ArgoCD UI by pointing to this repo’s URL.

ArgoCD will automatically start deploying the Helm chart.

---

## 🌐 Accessing the Application

After ArgoCD syncs, OpenShift creates a public **Route**.

Get it with:

```bash
oc get route
```

Open the host value in your browser to access your running application.

---

## 🧩 Key Features Implemented

### **1. Health Probes**

The Deployment uses:

* `/health/readiness`
* `/health/liveliness`

This ensures pods only receive traffic once the application is ready.

### **2. ConfigMap-Based HTML Page**

A small HTML file is stored in a ConfigMap and mounted at runtime:

```yaml
volumeMounts:
  - name: index-html
    mountPath: /tmp/html
```

### **3. Rolling Updates**

The chart uses a standard rolling update strategy:

```yaml
maxUnavailable: 25%
maxSurge: 25%
```

---

## 🔨 Helm Configuration

Update app parameters in:

```
charts/values.yaml
```

Examples:

```yaml
ReplicaNumber: 1

containers:
  image: quay.io/...
  tag: v1.0
  containerPort: 8080
```

---

## 🏫 About This Repository

This project was created during the **Red Hat OpenShift & GitOps training program**, in collaboration with the Isracard Digital Development team.

It demonstrates real-world practices for:

* GitOps automation
* Helm chart deployment
* OpenShift application delivery

---

## 🙌 Acknowledgments

Special thanks to:

**Shahaf Behar** – Red Hat Architect
For providing guidance, explanations, and best practices during the workshop.
