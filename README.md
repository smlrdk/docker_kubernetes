# docker_kubernetes
DevOps practice
1. ```docker build -t zhenyap/server:1.0.0 -t zhenyap/server:latest server``` - сборка docker image.
2. ```docker login -u smlrdk``` -  вход в docker hub.
3. ```docker push smlrdk/server:1.0.0``` - push image.
4. ```minikube start --driver=docker``` - запуск кластера миникуба.
5. ```kubectl apply -f deployment.yaml``` - установка манифэста.
6. ```kubectl get deployments``` - проверка успешного создания деплоймента. 
7. ```kubectl get pods``` - проверка успешного создания запущенных реплик.
8. ```kubectl port-forward --address 0.0.0.0 deployment/web 8080:8000``` - обеспечение доступа к веб-приложению внутри кластера. 
9. ```kubectl describe deployment web``` - проверка работоспособности текущего состояния деплоймента.

Результат:
```PS D:\Study\magistry\sem_2\DevOps\docker_kubernetes> kubectl describe deployment web
Name:                   web
Namespace:              default
CreationTimestamp:      Mon, 22 May 2023 22:30:39 +0300
Labels:                 app=server
Annotations:            deployment.kubernetes.io/revision: 1
Selector:               app=server
Replicas:               2 desired | 2 updated | 2 total | 2 available | 0 unavailable
StrategyType:           RollingUpdate
MinReadySeconds:        0
RollingUpdateStrategy:  25% max unavailable, 25% max surge
Pod Template:
  Labels:  app=server
  Containers:
   server:
    Image:        smlrdk/server:1.0.0
    Port:         8000/TCP
    Host Port:    0/TCP
    Liveness:     http-get http://:8000/hello.html delay=3s timeout=1s period=3s #success=1 #failure=3
    Environment:  <none>
    Mounts:       <none>
  Volumes:        <none>
Conditions:
  Type           Status  Reason
  ----           ------  ------
  Available      True    MinimumReplicasAvailable
  Progressing    True    NewReplicaSetAvailable
OldReplicaSets:  <none>
NewReplicaSet:   web-7fd8c58db6 (2/2 replicas created)
Events:
  Type    Reason             Age    From                   Message
  ----    ------             ----   ----                   -------
  Normal  ScalingReplicaSet  4m48s  deployment-controller  Scaled up replica set web-7fd8c58db6 to 2
```