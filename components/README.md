1. Set Pod Security Standard enforce=privileged `kubectl label ns daprspike-dev "pod-security.kubernetes.io/enforce"=privileged --overwrite`
1. Apply DAPR configuration. `kubectl apply -f ./appconfig.yaml`
1. Patch frontend with DAPR annotations. `kubectl patch deployments.apps -n daprspike-dev frontend --patch-file ./frontend.yaml`
1. Patch dotnet-sub with DAPR annotations. `kubectl patch deployments.apps -n daprspike-dev dotnet-sub --patch-file ./csharp-subscriber.yaml`