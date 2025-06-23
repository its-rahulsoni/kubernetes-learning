How to start Kubernetes Cluster locally ?

Got it! Since you're using **Windows** and already have **Minikube** and **kubectl** installed, let's go through **how to create a Kubernetes cluster** step-by-step using **PowerShell or Command Prompt** (no Bash commands).

---

## ✅ Step-by-Step: Create Minikube Cluster on Windows

### ✅ Step 1: Open PowerShell (or Command Prompt) **as Administrator**

---

### ✅ Step 2: Start Minikube Cluster

If you're using **Docker Desktop** as the backend:

```powershell
minikube start --driver=docker
```

Or if you're using **Hyper-V**:

```powershell
minikube start --driver=hyperv --hyperv-virtual-switch "Primary Virtual Switch"
```

> 📝 To list available drivers on your system:

```powershell
minikube drivers
```

If successful, you'll see output ending with something like:

```
🎉 Done! kubectl is now configured to use "minikube" cluster
```

---

### ✅ Step 3: Verify Cluster is Running

```powershell
kubectl get nodes
```

You should see:

```
NAME       STATUS   ROLES           AGE   VERSION
minikube   Ready    control-plane   ...   vX.X.X
```

---

### ✅ Step 4: Enable Ingress Controller (Optional, useful later)

```powershell
minikube addons enable ingress
```

---

### ✅ Step 5: Access Kubernetes Dashboard (Optional, for UI-based inspection)

```powershell
minikube dashboard
```

This will open a browser window with the full Kubernetes dashboard.

---

### ✅ Step 6: Use Minikube's Docker Daemon (for local image testing)

If you want to **build and use local Docker images inside the cluster**, run:

```powershell
minikube docker-env
```

Then, **copy-paste** the output from that command into your PowerShell to switch Docker context.

Example output:

```powershell
$env:DOCKER_TLS_VERIFY = "1"
$env:DOCKER_HOST = "tcp://127.0.0.1:57324"
$env:DOCKER_CERT_PATH = "C:\Users\<username>\.minikube\certs"
$env:MINIKUBE_ACTIVE_DOCKERD = "minikube"
```

Then run:

```powershell
docker build -t my-service:local .
```

You can now reference `my-service:local` inside your Kubernetes manifests.

---

### ✅ Step 7: Apply Manifests

Make sure your `deployment.yaml` and `service.yaml` are ready. Then:

```powershell
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```

To expose a service on the browser:

```powershell
minikube service my-service
```

---

Would you like me to:

* Generate a ready-to-use `deployment.yaml` and `service.yaml` for your service?
* Help set up a local Jenkins job that does the deployment?

Let me know how you'd like to proceed.
