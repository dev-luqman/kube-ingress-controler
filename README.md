# Introduction to ingress controller using nginx and aws elastic load balancer.

### Documentation Link

- [Nginx Ingress Documention](https://docs.nginx.com/nginx-ingress-controller/)
- [Nginx Ingress Helm chart Version](https://docs.nginx.com/nginx-ingress-controller/installation/installation-with-helm/)

### Helm repo commands

```

helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx

helm search repo ingress-nginx --versions

```

### Applications version

| packages | version | type        |
| -------- | ------- | ----------- |
| Kubectl  | 1.25.4  | Client      |
| kubectl  | 1.22.17 | server      |
| helm     | 4.4.0   | Chart       |
| helm     | 1.5.1   | App version |

### Variables

helm variables

```

CHART_VERSION = "4.4.0"
APP_VERSION = "1.5.0"

```

### Transfer nginx helm chart template to a directory

```

mkdir ./kubernetes_nginx/manifest/

helm template ingress-nginx ingress-nginx \
--repo https://kubernetes.github.io/ingress-nginx \
--version ${CHART_VERSION} \
--namespace nginx-ingress \
>  k8s_nginx/manifest/nginx-ingress.${APP_VERSION}.yml

```

helm template ingress-nginx ingress-nginx \
--repo https://kubernetes.github.io/ingress-nginx \
--version ${CHART_VERSION} --namespace nginx-ingress > kubernetes_nginx/manifest/nginx-ingress.${APP_VERSION}.yml
