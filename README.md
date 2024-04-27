The logs for commands run and their output in sequential order

@sum-sagar ➜ /workspaces/sre-week-four (project) $ minikube start
😄  minikube v1.32.0 on Ubuntu 20.04 (docker/amd64)
🎉  minikube 1.33.0 is available! Download it: https://github.com/kubernetes/minikube/releases/tag/v1.33.0
💡  To disable this notice, run: 'minikube config set WantUpdateNotification false'

✨  Automatically selected the docker driver. Other choices: none, ssh
📌  Using Docker driver with root privileges
👍  Starting control plane node minikube in cluster minikube
🚜  Pulling base image ...
💾  Downloading Kubernetes v1.28.3 preload ...
    > preloaded-images-k8s-v18-v1...:  403.35 MiB / 403.35 MiB  100.00% 16.42 M
    > gcr.io/k8s-minikube/kicbase...:  453.90 MiB / 453.90 MiB  100.00% 15.81 M
🔥  Creating docker container (CPUs=2, Memory=2200MB) ...
🐳  Preparing Kubernetes v1.28.3 on Docker 24.0.7 ...
    ▪ Generating certificates and keys ...
    ▪ Booting up control plane ...
    ▪ Configuring RBAC rules ...
🔗  Configuring bridge CNI (Container Networking Interface) ...
    ▪ Using image gcr.io/k8s-minikube/storage-provisioner:v5
🔎  Verifying Kubernetes components...
🌟  Enabled addons: storage-provisioner, default-storageclass
🏄  Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default

@sum-sagar ➜ /workspaces/sre-week-four (project) $ kubectl create namespace sre
namespace/sre created

@sum-sagar ➜ /workspaces/sre-week-four (project) $ helm install upcommerce ./upcommerce -n sre
NAME: upcommerce
LAST DEPLOYED: Sat Apr 27 09:06:07 2024
NAMESPACE: sre
STATUS: deployed
REVISION: 1
TEST SUITE: None

@sum-sagar ➜ /workspaces/sre-week-four (project) $ kubectl get deployment -n sre
NAME             READY   UP-TO-DATE   AVAILABLE   AGE
upcommerce-app   1/1     1            1           26s

@sum-sagar ➜ /workspaces/sre-week-four (project) $ helm upgrade upcommerce ./upcommerce -n sre
Release "upcommerce" has been upgraded. Happy Helming!
NAME: upcommerce
LAST DEPLOYED: Sat Apr 27 09:20:50 2024
NAMESPACE: sre
STATUS: deployed
REVISION: 2
TEST SUITE: None

@sum-sagar ➜ /workspaces/sre-week-four (project) $ kubectl get deployment -n sre -o wide
NAME                    READY   UP-TO-DATE   AVAILABLE   AGE   CONTAINERS   IMAGES                        SELECTOR
upcommerce-app          1/1     1            1           14m   upcommerce   uonyeka/upcommerce:v3         app=upcommerce-app
upcommerce-canary-app   0/1     1            0           15s   canary       uonyeka/canary:linux-amd-64   app=upcommerce-canary-app

@sum-sagar ➜ /workspaces/sre-week-four (project) $ kubectl get deployment -n sre -o wide
NAME                    READY   UP-TO-DATE   AVAILABLE   AGE   CONTAINERS   IMAGES                        SELECTOR
upcommerce-app          1/1     1            1           15m   upcommerce   uonyeka/upcommerce:v3         app=upcommerce-app
upcommerce-canary-app   0/1     1            0           31s   canary       uonyeka/canary:linux-amd-64   app=upcommerce-canary-app

@sum-sagar ➜ /workspaces/sre-week-four (project) $ kubectl get deployment -n sre -o wide
NAME                    READY   UP-TO-DATE   AVAILABLE   AGE   CONTAINERS   IMAGES                        SELECTOR
upcommerce-app          1/1     1            1           15m   upcommerce   uonyeka/upcommerce:v3         app=upcommerce-app
upcommerce-canary-app   0/1     1            0           50s   canary       uonyeka/canary:linux-amd-64   app=upcommerce-canary-app

@sum-sagar ➜ /workspaces/sre-week-four (project) $ helm upgrade upcommerce ./upcommerce -n sre
Release "upcommerce" has been upgraded. Happy Helming!
NAME: upcommerce
LAST DEPLOYED: Sat Apr 27 09:22:07 2024
NAMESPACE: sre
STATUS: deployed
REVISION: 3
TEST SUITE: None

@sum-sagar ➜ /workspaces/sre-week-four (project) $ helm list -a -n sre 
NAME            NAMESPACE       REVISION        UPDATED                                 STATUS          CHART                   APP VERSION
upcommerce      sre             3               2024-04-27 09:22:07.322612651 +0000 UTC deployed        upcommerce-0.1.0                   

@sum-sagar ➜ /workspaces/sre-week-four (project) $ kubectl get deployment -n sre -o wide
NAME                    READY   UP-TO-DATE   AVAILABLE   AGE    CONTAINERS   IMAGES                        SELECTOR
upcommerce-app          1/1     1            1           16m    upcommerce   uonyeka/upcommerce:v3         app=upcommerce-app
upcommerce-canary-app   0/1     1            0           106s   canary       uonyeka/canary:linux-amd-64   app=upcommerce-canary-app

@sum-sagar ➜ /workspaces/sre-week-four (project) $ helm list -a -n sre 
NAME            NAMESPACE       REVISION        UPDATED                                 STATUS          CHART                   APP VERSION
upcommerce      sre             3               2024-04-27 09:22:07.322612651 +0000 UTC deployed        upcommerce-0.1.0                   

@sum-sagar ➜ /workspaces/sre-week-four (project) $ helm history upcommerce -n sre
REVISION        UPDATED                         STATUS          CHART                   APP VERSION     DESCRIPTION     
1               Sat Apr 27 09:06:07 2024        superseded      upcommerce-0.1.0                        Install complete
2               Sat Apr 27 09:20:50 2024        superseded      upcommerce-0.1.0                        Upgrade complete
3               Sat Apr 27 09:22:07 2024        deployed        upcommerce-0.1.0                        Upgrade complete

@sum-sagar ➜ /workspaces/sre-week-four (project) $ helm list -a -n sre
NAME            NAMESPACE       REVISION        UPDATED                                 STATUS          CHART                   APP VERSION
upcommerce      sre             3               2024-04-27 09:22:07.322612651 +0000 UTC deployed        upcommerce-0.1.0                   

@sum-sagar ➜ /workspaces/sre-week-four (project) $ helm history upcommerce -n sre
REVISION        UPDATED                         STATUS          CHART                   APP VERSION     DESCRIPTION     
1               Sat Apr 27 09:06:07 2024        superseded      upcommerce-0.1.0                        Install complete
2               Sat Apr 27 09:20:50 2024        superseded      upcommerce-0.1.0                        Upgrade complete
3               Sat Apr 27 09:22:07 2024        deployed        upcommerce-0.1.0                        Upgrade complete

@sum-sagar ➜ /workspaces/sre-week-four (project) $ helm ls -n sre    # List all releases (deployments).

NAME        NAMESPACE       REVISION        UPDATED                                 STATUS          CHART           APP VERSION
upcommerce      sre             3               2024-04-27 09:22:07.322612651 +0000 UTC deployed        upcommerce-0.1.0                   

@sum-sagar ➜ /workspaces/sre-week-four (project) $ helm status upcommerce -n sre   # Get detailed information about a specific release.
NAME: upcommerce
LAST DEPLOYED: Sat Apr 27 09:22:07 2024
NAMESPACE: sre
STATUS: deployed
REVISION: 3
TEST SUITE: None

@sum-sagar ➜ /workspaces/sre-week-four (project) $ helm uninstall upcommerce -n sre  # Uninstall a release.
release "upcommerce" uninstalled

@sum-sagar ➜ /workspaces/sre-week-four (project) $ helm history upcommerce -n sre  # View the revision history of a release.
Error: release: not found

@sum-sagar ➜ /workspaces/sre-week-four (project) $ helm show values ./upcommerce -n sre  # Display default values from the chart.
replicaCount: 1
imagePullPolicy: Always
cpuLimit: "1"
memoryLimit: "4Gi"
upcommerce:
  image: uonyeka/upcommerce:v3
canary:
  image: uonyeka/canary:linux-amd-64
  
@sum-sagar ➜ /workspaces/sre-week-four (project) $ helm lint ./upcommerce -n sre  # Check your chart for issues.
==> Linting ./upcommerce
[INFO] Chart.yaml: icon is recommended

1 chart(s) linted, 0 chart(s) failed

@sum-sagar ➜ /workspaces/sre-week-four (project) $ helm template upcommerce ./upcommerce -n sre  # Render templates without installing.
---
# Source: upcommerce/templates/canary-deployment.yaml
apiVersion: v1
kind: Service
metadata:
    name: upcommerce--canary-service
spec:
    selector:
      app: upcommerce--canary-app
    ports:
      - protocol: TCP
        port: 5003
        targetPort: 5003
---
# Source: upcommerce/templates/service.yaml
apiVersion: v1
kind: Service
metadata:
  name: upcommerce-service
spec:
  selector:
    app: upcommerce-app
  ports:
    - protocol: TCP
      port: 5000
      targetPort: 5000
  type: NodePort
---
# Source: upcommerce/templates/canary-service.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: upcommerce-canary-app
spec:
  replicas: 1
  selector:
    matchLabels:
      app: upcommerce-canary-app
  template:
    metadata:
      labels:
        app: upcommerce-canary-app
    spec:
      containers:
        - name: canary
          image: uonyeka/canary:linux-amd-64
          ports:
            - containerPort: 5003
          imagePullPolicy: Always
          resources:
            limits:
              cpu: 1
              memory: 4Gi
---
# Source: upcommerce/templates/deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: upcommerce-app
spec:
  replicas: 1
  selector:
    matchLabels:
      app: upcommerce-app
  template:
    metadata:
      labels:
        app: upcommerce-app
    spec:
      containers:
        - name: upcommerce
          image: uonyeka/upcommerce:v3
          ports:
            - containerPort: 5000
          imagePullPolicy: Always
          resources:
            limits:
              cpu: 1
              memory: 4Gi


