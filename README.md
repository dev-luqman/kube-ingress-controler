# Introduction to ingress controller using nginx and aws elastic load balancer.

---

> Configuration to multiple microservices using ingress controller and aws loadbalancer

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
>  kubernetes_nginx/manifest/nginx-ingress.${APP_VERSION}.yml

```

### Deploy the ingress controller

```
kubectl create namespace nginx-ingress

kubectl apply -f  kubernetes_nginx/manifest/nginx-ingress.1.5.0.yml

```

### Confirm installation

```
kubectl -n nginx-ingress get pods

```

```
NAME READY STATUS RESTARTS AGE
ingress-nginx-admission-create-q4hrk 0/1 Completed 0 3m23s
ingress-nginx-admission-patch-g5kp6 0/1 Completed 1 3m22s
ingress-nginx-controller-666f45c794-9qf8g 1/1 Running 0 3m28s
```

Confirming the created loadbalancer through svc

```
kubectl -n nginx-ingress get svc
```

```
NAME                                 TYPE           CLUSTER-IP       EXTERNAL-IP                                                               PORT(S)                      AGE
ingress-nginx-controller             LoadBalancer   10.100.175.182   a3891302e57834bce913e7d04bb94394-2063151079.us-east-1.elb.amazonaws.com   80:32592/TCP,443:31877/TCP   12m
ingress-nginx-controller-admission   ClusterIP      10.100.200.26    <none>                                                                    443/TCP                      12m
```
