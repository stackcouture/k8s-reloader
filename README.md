## 🔄 Automating Kubernetes Config & Secret Reloads with Stakater Reloader

A hands-on demo showing how to automatically reload Kubernetes Deployments when **ConfigMaps** or **Secrets** are updated — powered by **[Stakater Reloader](https://github.com/stakater/Reloader)**.

---

### 📘 Overview

In traditional Kubernetes workflows, updating a ConfigMap or Secret doesn’t automatically trigger a pod restart — meaning your app may continue running with **stale configuration values**.

**Stakater Reloader** solves this by watching ConfigMaps and Secrets. Whenever a change is detected, it triggers a **rolling restart** of any associated Deployment, StatefulSet, or DaemonSet.

---

### 🧩 Demo Architecture

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
