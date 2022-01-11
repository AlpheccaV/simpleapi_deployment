# Технологии разработки программного обеспечения  
## Лабораторная работа №2: создание кластера Kubernetes и деплой приложения
- Разработчик: Инюткина А.С.
- Группа: МБД 2131
- Цель лаб.работы: знакомство с кластерной архитектурой на примере Kubernetes, а также деплоем приложения в кластер.

### Манифест deployment.yaml

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-deployment
spec:
  replicas: 10
  selector:
    matchLabels:
      app: my-app
  strategy:
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 1
    type: RollingUpdate
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
        - image: myapi:latest
          name: myapi
          imagePullPolicy: Never
          ports:
            - containerPort: 8080
      hostAliases:
      - ip: "192.168.49.1" # The IP of localhost from MiniKube
        hostnames:
        - postgres.local
```

### Манифест service.yaml

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  type: NodePort
  ports:
    - nodePort: 31317
      port: 8080
      protocol: TCP
      targetPort: 8080
  selector:
    app: my-app
```

### Скрин подов из консоли
<img src=''>

### Скрин подов в дашборде
<img src=''>

### Обзор кластера
[Линк](link here)
