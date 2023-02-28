## Разворачивание кластера

- Создание пространств имён
```shell
kubectl apply -f ./namespaces.yaml
```

- Установка cert-manager, создание self-signed cluster issuer
```shell
helm install cert-manager jetstack/cert-manager --set installCRDs=true --namespace security
kubectl apply -f ./cert-manager/resources.yaml
```

- Установка nginx-ingress
```shell
helm install nginx-ingress ingress-nginx/ingress-nginx --namespace nginx-ingress
```

- Установка Keycloak
```shell
helm install keycloak bitnami/keycloak -f ./keycloak/keycloak-values.yaml --namespace security
```

- Установка PostgreSQL для сервиса:
```shell
kubectl apply -f ./db/resources.yaml
helm install postgresql -f ./db/postgresql-values.yaml bitnami/postgresql --namespace otus-user
```

- Установка сервиса:
```shell
kubectl apply -f ./service-user/resources.yaml
```
