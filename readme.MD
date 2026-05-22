# MongoDB

We use bastion host as Docker server and EKS client.
Make sure `aws configure` is done in bastion and connected to EKS cluster.
```
aws eks update-kubeconfig --region us-east-1 --name roboshop-dev
```
```
kubectl create namespace roboshop
```
* Login to ECR
```
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 315069654700.dkr.ecr.us-east-1.amazonaws.com
```
* Build MongoDB image.
```
docker build -t 655431895664.dkr.ecr.us-east-1.amazonaws.com/roboshop/dev/mongodb:v1.0.2 .
```
* Push image
```
docker push 655431895664.dkr.ecr.us-east-1.amazonaws.com/roboshop/dev/mongodb:v1.0.2
```
* Now install using Helm. move to helm directory
```
helm upgrade --install mongodb . -n roboshop
```
* go to roboshop namespace
```
 kubens roboshop
 `````
 * check pods
 
 ```
  ec2-user@ip-10-0-1-110 ~/mongodb/helm ]$ kubectl get pods
NAME                       READY   STATUS    RESTARTS   AGE
mongodb-86dc56f8fb-9twtq   1/1     Running   0          4m15s


 ```