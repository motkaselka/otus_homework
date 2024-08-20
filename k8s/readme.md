Манифесты для деплоя в k8s сервиса.
Манифесты описывают сущности: Deployment, Service, Ingress.

1) Запустить minikube:
minikube start

2) Деплой NGINX Ingress Controller:
kubectl create namespace m && helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx/ && helm repo update && helm install nginx ingress-nginx/ingress-nginx --namespace m -f nginx-ingress.yaml

3) Деплой сервиса:
kubectl apply -f Deployment.yaml
kubectl apply -f Service.yaml
kubectl apply -f Ingress.yaml

4) Настроить /etc/hosts: 
Добавьте запись в файл /etc/hosts:
{minikube_ip} arch.homework
Где {minikube_ip} - это IP адрес minikube. Получить IP адрес, выполнив команду:
minikube ip

5) Проверить сервисы
curl http://arch.homework/health
curl http://arch.homework/otusapp/dmitriev/health

Запрос на http://arch.homework/otusapp/dmitriev/health отдает {“status”: “OK”}.

Для удаления всех созданных ресурсов нужно выполнить следующие команды:
kubectl delete -f ingress.yaml
kubectl delete -f service.yaml
kubectl delete -f deployment.yaml
helm uninstall nginx --namespace m
kubectl delete namespace m
