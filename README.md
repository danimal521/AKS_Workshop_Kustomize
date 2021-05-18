# AKS Workshop Kustomize

## Introduction


Kubernetes relies on YAML for deployment definitions. As you applications grow and more services, application and namespaces are added, these YAML definitions can become hard to manage. Add several different environments such as UAT and Production and DevOps, mistakes to your cluster are inevitable. 

[kustomize](https://kustomize.io/#overview) is built-in to kubectl and assists in managing templates.


The main concepts in Kustomize are "bases" and "overlays" ([terms](https://kubectl.docs.kubernetes.io/references/kustomize/glossary/)). The idea is to have a "base" desired state such as "UAT" where the YMAL might include a small node pool and ingress. Then you might have a "production overlay" where you have a large cluster in a different namespace.

This module will guide you through the tutorial below to give you hands-on experience configuring and using Kustomize to templatize a YAML workload.


## Tutorial: Redeploy ngnix
_(5 minutes)_

In this tutorial we will deploy a simple YAML from the [PVC](https://github.com/rickrain/k8s-volumes/blob/main/README.md#tutorial-pod-storage) demo. This is a simple NGNIX container with no customizations. Make sure you have the [01-pod-storage.yaml](https://github.com/rickrain/k8s-volumes/blob/main/01-pod-storage.yaml).

### Step-by-step instructions

Execute the commands below from a bash command shell. Assure you are in the directory with your YAML.

```bash
# Apply deployment to the cluster
kubectl apply -f 01-pod-storage.yaml

# List the pod that was created
kubectl get pods

# Setup port forwarding so you can browse to the running container.
# Replace '[pod-name]' with the name of your pod.
kubectl port-forward [pod-name] 8080:80

# Open browser to localhost:8080.
# Observe that the response is the standard 'Welcome to nginx!' response.

# Press Ctrl-c to terminate the port forwarding.

# Delete the deployment
kubectl delete -f 01-pod-storage.yaml
```

