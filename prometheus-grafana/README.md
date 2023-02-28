## Home Work 3 Olena Ivina
### Prometheus & Grafana

Project structure:
```
.
├── compose.yaml
├── kubernetes
│   └── grafana-configmap.yml
│   └── grafana-deployment.yml
│   └── grafana-service.yml
│   └── prometheus-configmap.yml
│   └── prometheus-deployment.yml
│   └── prometheus-grafana-networkpolicy.yml
│   └── prometheus-persistentvolumeclaim.yml
│   └── prometheus-service.yml
│   └── secret.yml
├── grafana
│   └── datasource.yml
├── prometheus
│   └── prometheus.yml
└── README.md
```

[_compose.yaml_](compose.yaml)
```
services:
  prometheus:
    image: prom/prometheus
    ...
    ports:
      - 9090:9090
  grafana:
    image: grafana/grafana
    ...
    ports:
      - 3000:3000
```
The compose file defines a stack with two services `prometheus` and `grafana`.
When deploying the stack, docker compose maps port the default ports for each service to the equivalent ports on the host in order to inspect easier the web interface of each service.
Make sure the ports 9090 and 3000 on the host are not already in use.

## Deploy Minikube

```
Requirements:

minikube
kompose

To do:

1) get repo from https://github.com/docker/awesome-compose/tree/master/prometheus-grafana
2) $ minikube start from the folder 
3) kompose convert -f compose.yaml -o kubernetes/
4) Create secret.yml 
5) Create prometheus-configmap.yml and grafana-configmap.yml and configure with datasource.yml and prometheus.yml accordinnaly 
6) kubectl apply -f kubernetes/

To access the grafana UI run:
7) minikube service grafana



```

## Expected result

Running kubectl get all you will get
```
pod/grafana-6455fb6bff-ncxbl      1/1     Running   0          27m
pod/prometheus-59c86c69b7-lrgwq   1/1     Running   0          27m

NAME                 TYPE           CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
service/grafana      LoadBalancer   10.102.192.128   <pending>     3000:30447/TCP   27m
service/kubernetes   ClusterIP      10.96.0.1        <none>        443/TCP          28m
service/prometheus   LoadBalancer   10.110.151.137   <pending>     9090:32354/TCP   27m

NAME                         READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/grafana      1/1     1            1           27m
deployment.apps/prometheus   1/1     1            1           27m

NAME                                    DESIRED   CURRENT   READY   AGE
replicaset.apps/grafana-6455fb6bff      1         1         1       27m
replicaset.apps/prometheus-59c86c69b7   1         1         1       27m
```


Stop and remove the minikube
```
$ minikube delete --all
```
