# Kubernetes Cheat Sheet

[Overview](https://kubernetes.io/docs/reference/kubectl/overview/), [Installation](https://kubernetes.io/docs/tasks/tools/install-kubectl/), [Reference](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)

## General information

```bash
# display version
kubectl version

# display cluster information
kubectl cluster-info

# display cluster configuration
kubectl config get-clusters

# display context configuration
kubectl config get-contexts

# change context
kubectl config use-context <cluster-name>
```

## Resources

### Nodes

```bash
# list nodes
kubectl get nodes
```

### Pods

```bash
# list pods of a specific namespace
kubectl get pods --namespace kube-system

# list pods of all namespaces
kubectl get pods -A

# get more information about a pod
kubectl describe pod

# get log information of a specific pod
kubectl logs

# get pod yaml definition
kubectl get pod -o yaml

# watch pods
watch kubectl get pod --all-namespaces

# desribe a pod
kubectl describe pod <pod-name> --namespace <namespace>
```

### ServiceAccounts

```bash
# see all service accounts in all namespaces
kubectl get ServiceAccount -A
```

### Definitions

#### CustomResourceDefinition

### RBAC

#### ClusterRole

#### ClusterRoleBinding

#### Role

#### RoleBinding

### MutatingWebhookConfiguration

### ValidatingWebhookConfiguration

### Secrets

```bash
# see all secrets in all namespaces
kubectl get secrets -A
```

### ConfigMap

### Deployments

```bash
kubectl get deployment
```

### Services

```bash
# see all services in all namespaces
kubectl get services -A
```

### Events

```bash
kubectl get events --sort-by=.metadata.creationTimestamp
```

### Ingress

```bash
# see all ingresses in all namespaces
kubectl get ingress -A

# see a resource definition
kubectl get ingress mymicroservice -o yaml
```

## Actions

### Scale

```bash
kubectl scale
```

## Port forwarding

```bash
kubectl port-forward xxx 8080:80
```

## Clean-up

```bash
# delete what was deployed by a manifest file
kubectl delete -f ./definition.json
```

## Proxy

```bash
# runs a proxy to the Kubernetes API Server
kubectl proxy
```

## Service provider

### Azure Kubernetes Service (AKS)

```bash
# review agent pool specification
az aks show --resource-group myrgname --name myaksname --query agentPoolProfiles

# scale agent pool (2 nodes here)
az aks scale --resource-group myrgname --name myaksname --node-count 2 --query properties.provisioningState
```

## Recipes

### Quick fixes

```bash
# find and delete pods
kubectl delete pods $(kubectl get pods -o=name | grep mypodname | sed "s/^.\{4\}//")
```

### Known issues

Issue | Advice
----- | ------
Pod with status `CreateContainerConfigError` | Look at the pod logs (`kubectl logs podxxx`), the issue should be detailed there