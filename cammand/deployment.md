
kubectl apply -f .\mysql-deployment.yaml
 ## deployment.apps/mysql-deployment created
service/mysql-service created
kubectl apply -f .\jbpm-deployment.yaml
deployment.apps/jbpm-deployment created
service/jbpm-service created
kubectl apply -f .\camel-deployment.yaml
deployment.apps/camel-deployment created
service/camel-service created
