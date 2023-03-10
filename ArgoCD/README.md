# Установка ArgoCD в Kubernetes
Установим ArgoCD с помощью helm
```
kubectl create namespace argocd
helm repo add argo https://argoproj.github.io/argo-helm
helm search repo argocd -l
helm install argocd argo/argo-cd -n argocd --version 5.17.1
```
Изменим сервис на NodePort:
```
kubectl get svc -n argocd
EDITOR='nano' kubectl -n argocd edit svc argocd-server
```
```
type: NodePort
```

Зайдем в ArgoCD  в браузере, отсюда возмем IP адрес:
```
kubectl get no -o wide
```

Отсюда возмем порт:
```
get svc -n argocd
```
Логин: *admin*

Пароль взять отсюда:
```
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 --decode && echo
```