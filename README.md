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

- Установка nginx-ingress-controller:
```shell
helm install nginx-ingress ingress-nginx/ingress-nginx --namespace nginx-ic
```

- Установка Keycloak
```shell
helm install keycloak bitnami/keycloak -f ./keycloak/keycloak-values.yaml --namespace security
```

- Установка oauth2-proxy
```shell
helm install oauth2-proxy oauth2-proxy/oauth2-proxy -f ./oauth2-proxy/oauth2-proxy-values.yaml --namespace rev-proxy
```

- Установка PostgreSQL для сервиса:
```shell
kubectl apply -f ./db/resources.yaml
helm install postgresql -f ./db/postgresql-values.yaml bitnami/postgresql --namespace otus-user
```

- Установка сервиса:
```shell
kubectl apply -f ./service-user/resources.yaml
kubectl apply -f ./service-user/ingress.yaml
```

- Установка UI:
```shell
kubectl apply -f ./frontend-user/resources.yaml
kubectl apply -f ./frontend-user/ingress.yaml
```