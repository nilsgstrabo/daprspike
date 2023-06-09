# Install DAPR

```shell
helm upgrade --install dapr dapr/dapr \
--version=1.10 \
--namespace dapr-system \
--create-namespace \
--wait
```

# Post deployment steps

After each deployment to Radix, apply the following scripts. This will disable Pod Security Policy for the namespace and add required annotations to deployments to inject DAPR sidecars.

1. Set Pod Security Standard enforce=privileged `kubectl label ns daprspike-dev "pod-security.kubernetes.io/enforce"=privileged --overwrite`
1. Create secret containing redis password. `kubectl create secret generic dapr-redis -n daprspike-dev --from-literal=redis_pwd=wrongpwd --dry-run=client -oyaml | kubectl apply -f -`
1. Apply RBAC. `kubectl apply -f ./rbac.yaml`
1. Apply DAPR configuration. `kubectl apply -f ./appconfig.yaml`
1. Apply pubsub redis configuration. `kubectl apply -f ./redis.yaml`
1. Patch frontend with DAPR annotations. `kubectl patch deployments.apps -n daprspike-dev frontend --patch-file ./frontend.yaml`
1. Patch dotnet-sub with DAPR annotations. `kubectl patch deployments.apps -n daprspike-dev dotnet-sub --patch-file ./csharp-subscriber.yaml`
1. Patch node-sub with DAPR annotations. `kubectl patch deployments.apps -n daprspike-dev node-sub --patch-file ./node-subscriber.yaml`
1. Patch python-sub with DAPR annotations. `kubectl patch deployments.apps -n daprspike-dev python-sub --patch-file ./python-subscriber.yaml`

All scripts combined:

```shell
kubectl label ns daprspike-dev "pod-security.kubernetes.io/enforce"=privileged --overwrite
kubectl apply -f ./appconfig.yaml
kubectl create secret generic dapr-redis -n daprspike-dev --from-literal=redis_pwd=12345 --dry-run=client -oyaml | kubectl apply -f -
kubectl apply -f ./rbac.yaml
kubectl apply -f ./redis.yaml
kubectl patch deployments.apps -n daprspike-dev frontend --patch-file ./frontend.yaml
kubectl patch deployments.apps -n daprspike-dev dotnet-sub --patch-file ./csharp-subscriber.yaml
kubectl patch deployments.apps -n daprspike-dev node-sub --patch-file ./node-subscriber.yaml
kubectl patch deployments.apps -n daprspike-dev python-sub --patch-file ./python-subscriber.yaml
```
