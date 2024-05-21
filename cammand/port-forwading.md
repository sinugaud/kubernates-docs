 kubectl  get svc mysql-service

 kubectl port-forward svc/mysql-service 3306:3306

 kubectl  get svc camel-service

 kubectl port-forward svc/camel-service 8089:8089

PS D:\Salesforce_apache_camel\kubenates\cammands> kubectl get svc jbpm-service
NAME           TYPE       CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
jbpm-service   NodePort   10.103.36.205   <none>        8080:32387/TCP   4m28s
PS D:\Salesforce_apache_camel\kubenates\cammands> kubectl port-forward svc/jbpm-service 8080:8080