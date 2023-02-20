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

```shell
helm install keycloak bitnami/keycloak -f ./keycloak/keycloak-values.yaml --namespace security
```