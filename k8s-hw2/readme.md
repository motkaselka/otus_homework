Приложение упаковано в docker image:
https://hub.docker.com/repository/docker/motkaselka/my_crud_app

1) Запустить minikube:
```
minikube start
```
2) Создать новый namespace:
```
kubectl create namespace myapp-namespace
```
3) Деплой NGINX Ingress Controller:
```
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update
helm install my-ingress ingress-nginx/ingress-nginx --namespace myapp-namespace
```

4) Деплой PostgreSQL:
```
helm repo add bitnami https://charts.bitnami.com/bitnami
helm install mydb bitnami/postgresql -f db-values.yaml --namespace myapp-namespace
```

5) Деплой сервиса:
```
helm install my-crud-app ./my-crud-app
```

6) Запуск туннеля:
```
minikube tunnel
```

7) Проверка работы сервиса через newman: 
```
newman run simple-flask-app.postman_collection.json
```