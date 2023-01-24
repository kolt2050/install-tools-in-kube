# Установка ArgoCD в Kubernetes
Установим ArgoCD с помощью helm
```
k create namespace argocd
helm repo add argo https://argoproj.github.io/argo-helm
helm search repo argocd -l
helm install argocd argo/argo-cd -n argocd --version 5.17.1
```
Изменим сервис на NodePort:
```
k get svc -n argocd
EDITOR='nano' kubectl -n argocd edit svc argocd-server
```
```
type: NodePort
```

Зайдем в ArgoCD  в браузере, отсюда возмем IP адрес:
```
k get no -o wide
```

Отсюда возмем порт:
```
get svc -n argocd
```