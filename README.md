### 🔄 Automating Kubernetes Config & Secret Reloads with Stakater Reloader

A hands-on demo showing how to automatically reload Kubernetes Deployments when **ConfigMaps** or **Secrets** are updated — powered by **[Stakater Reloader](https://github.com/stakater/Reloader)**.

---

#### 📘 Overview

In traditional Kubernetes workflows, updating a ConfigMap or Secret doesn’t automatically trigger a pod restart — meaning your app may continue running with **stale configuration values**.

**Stakater Reloader** solves this by watching ConfigMaps and Secrets. Whenever a change is detected, it triggers a **rolling restart** of any associated Deployment, StatefulSet, or DaemonSet.

---

#### Demo Architecture

```text
+--------------------+
|  ConfigMap / Secret|   ← Edit values (ex: DB_URL, API_KEY)
+--------------------+
            |
            ▼
  Stakater Reloader detects change
            |
            ▼
  Deployment automatically restarts pods
            |
            ▼
+--------------------+
|   Application Pod  | → Runs with updated environment
+--------------------+
```
---
#### ⚙️ Tools & Environment
```text
-----------------|----------------------------------------------
| **Component**  | **Version / Description**                   |
|----------------|---------------------------------------------|
| **Kubernetes** | v1.28+ (KodeKloud Lab)                      |
| **Reloader**   | Stakater Reloader (latest Helm or manifest) |
| **Demo App**   | Simple deployment using ConfigMap           |
|----------------|---------------------------------------------|
```
---
#### Workflow

1. **Deploy Stakater Reloader** in your cluster.  
2. **Deploy your demo application** and **ConfigMap**.  
3. **Annotate the Deployment** to enable Reloader:

   ```yaml
   metadata:
     annotations:
       configmap.reloader.stakater.com/reload: "postgres-config"
       secret.reloader.stakater.com/reload: "postgres-secret"
    ```
 4. **Modify the ConfigMap** Reloader will automatically restart the affected pod.

 ##### Example 
 ```bash 
    kubectl apply -f configmap.yaml
    kubectl apply -f deployment.yaml
    kubectl apply -f reloader.yaml   
    kubectl edit configmap demo-config  
    kubectl get pods -w               
 ```
 ---

#### Real-World Integration

##### ✅ Works Great With

1. **GitOps Pipelines** — Automatically apply configuration changes from Git commits.  
2. **External Secrets Operator** — Integrates seamlessly with AWS Secrets Manager or HashiCorp Vault for secret rotations.  
3. **CI/CD Automation** — Ensures configuration and secret synchronization happens automatically.  
4. **Zero-Downtime Deployments** — Enables smooth rollouts without manual pod restarts.

---
