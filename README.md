# k8s-cheat-sheat

Install kubectl and minikube
```bash
winget install -e --id Kubernetes.kubectl
winget install -e --id Kubernetes.minikube
```

Start/stop/dashboard minikube
```bash
minikube start
minikube stop
minikube dashboard
```

Create namespaces
```bash
kubectl create namespace dev
```

Create pod
```bash
kubectl apply -f curl-pod.yaml -n dev
kubectl apply -f simple-nginx.yaml -n dev 
```

Delete pod
```bash
kubectl delete pod curl-pod -n dev
kubectl delete pod simple-nginx -n dev
```

Describe pod
```bash
kubectl describe pod curl-pod -n dev
kubectl describe pod simple-nginx -n dev
```

Log pod
```bash
kubectl logs curl-pod -n dev
kubectl logs simple-nginx -n dev
```

Connect to a pod
```bash
kubectl exec -n dev -it curl-pod -- sh
```


Call pods from different namespaces
```bash
kubectl describe pod simple-nginx -n prod | grep IP

kubectl -n dev exec curl-pod -- curl -I http://10.244.120.69
kubectl -n prod exec curl-pod -- curl -I http://10.244.120.69
```

Create network policy (needs CNI to be enforced):
```bash
minikube start --cni=calico
kubectl get pods -n kube-system

kubectl apply -f prod-ingress.yaml -n prod
```

Delete network policy:
```bash
kubectl delete networkpolicy prod-ingress -n prod
```

Get network policies:
```bash
kubectl get networkpolicy -n prod
```

Add ingress addons to minikube:
```bash
minikube addons enable ingress
```

Add Argo Rollouts:
```bash
kubectl create ns argo-rollouts 
kubectl apply -n argo-rollouts -f https://raw.githubusercontent.com/argoproj/argo-rollouts/stable/manifests/install.yaml 
```

Secrets:
```bash
kubectl get secret my-secret -n dev -o=jsonpath='{.data.password}' | base64 --decode
```
