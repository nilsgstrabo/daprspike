1. Set Pod Security Standard enforce=privileged `kubectl label ns daprspike-dev "pod-security.kubernetes.io/enforce"=privileged --overwrite`
1. Apply DAPR configuration. `kubectl apply -f ./appconfig.yaml`
1. Patch frontend with DAPR annotations. `kubectl patch deployments.apps -n daprspike-dev frontend --patch-file ./frontend.yaml`
1. Patch dotnet-sub with DAPR annotations. `kubectl patch deployments.apps -n daprspike-dev dotnet-sub --patch-file ./csharp-subscriber.yaml`
1. Patch node-sub with DAPR annotations. `kubectl patch deployments.apps -n daprspike-dev node-sub --patch-file ./node-subscriber.yaml`
1. Patch python-sub with DAPR annotations. `kubectl patch deployments.apps -n daprspike-dev python-sub --patch-file ./python-subscriber.yaml`

All scripts combined:

```shell
kubectl label ns daprspike-dev "pod-security.kubernetes.io/enforce"=privileged --overwrite
kubectl apply -f ./appconfig.yaml
kubectl patch deployments.apps -n daprspike-dev frontend --patch-file ./frontend.yaml
kubectl patch deployments.apps -n daprspike-dev dotnet-sub --patch-file ./csharp-subscriber.yaml
kubectl patch deployments.apps -n daprspike-dev node-sub --patch-file ./node-subscriber.yaml
kubectl patch deployments.apps -n daprspike-dev python-sub --patch-file ./python-subscriber.yaml
```