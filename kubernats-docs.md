  make sure you have isntall kubectl and minikube (tools for kubernate ) we can use other one also
here link to installtion
https://kubernetes.io/docs/tasks/tools/ install kubectl 
 install minikube 
 https://minikube.sigs.k8s.io/docs/handbook/kubectl/
 make sure you have docker install installtion


### Start Minikube and Basic Commands

```shell
minikube start
kubectl version
minikube dashboard
```

### Docker Commands

```shell
docker build -t your-docker-repo/your-app-name:tag .
docker login
docker push your-docker-repo/your-app-name:tag
```

### Apply Kubernetes Deployment

```shell
kubectl apply -f your-k8s-deployment.yaml
```

### Create a Kubernetes Secret

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: my-secret
type: Opaque
data:
  username: new-base64-encoded-username
  password: new-base64-encoded-password
```

```shell
kubectl apply -f new-secret.yaml
```

### Kubernetes Deployment with Environment Variables from a Secret

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app
spec:
  template:
    spec:
      containers:
      - name: my-app-container
        image: my-app-image
        env:
        - name: MY_USERNAME
          valueFrom:
            secretKeyRef:
              name: my-secret
              key: username
        - name: MY_PASSWORD
          valueFrom:
            secretKeyRef:
              name: my-secret
              key: password
```

### Multi-Container Kubernetes Deployment

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
        - name: spring-boot-app
          image: your-spring-boot-image:latest
          ports:
            - containerPort: 8080
        - name: jbpm-container
          image: your-jbpm-image:7.74.1
          # Add any additional configuration for the jbpm container
```

### Create Kubernetes Secret from Literal Values

```shell
kubectl create secret generic my-app-secrets \
  --from-literal=camel.component.salesforce.username=sinu@rutusoft.box \
  --from-literal=camel.component.salesforce.password=giSLWapKq8tTzwhyMSNSxCjm4UGBEVO1FRTmEk7 \
  --from-literal=camel.component.salesforce.clientId=3MVG95mg0lk4bathVhLOCxlLvz6hXaKpJ40tLwoRgJaPPpYhLAV57SG5zQjncrl5ot3f_BGHz6iAMAApIZ8is \
  --from-literal=camel.component.salesforce.clientSecret=7F10E6AC9A378D59DFB79CA7237F7D7F15131B1C6CDAF277C7F092CDEEA8D7E9 \
  --from-literal=camel.component.salesforce.loginUrl=https://rutusoft-dev-ed.develop.my.salesforce.com \
  --from-literal=jbpm.server.user=krisv \
  --from-literal=jbpm.server.pass=krisv
```

### Create Kubernetes Secret from Files

1. Create files on your local machine containing sensitive data.
2. Use `kubectl` to create a secret from the files:

```shell
kubectl create secret generic my-app-files-secrets \
  --from-file=salesforce-credentials.properties \
  --from-file=other-file.properties
```

### Mount the Secret as Volumes in Kubernetes Deployment

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app
spec:
  containers:
    - name: my-app-container
      image: my-app-image:tag
      volumeMounts:
        - name: app-secrets
          mountPath: /app/secrets
  volumes:
    - name: app-secrets
      secret:
        secretName: my-app-files-secrets
```

This setup mounts the `my-app-files-secrets` secret as a volume at `/app/secrets` in your Spring Boot application container.

You can then read the sensitive data from these mounted files within your container at runtime.

Additional Resource:
- [Managing Secrets Using Config Files](https://kubernetes.io/docs/tasks/configmap-secret/managing-secret-using-config-file/)

Please replace placeholders with your actual values and file names as needed.