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

- Установка Traefik:
```shell
helm install traefik traefik/traefik --namespace traefik
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
kubectl apply -f ./service-user/ingress.yaml
```