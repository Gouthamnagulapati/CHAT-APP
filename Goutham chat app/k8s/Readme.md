- Create a namespace

```bash

jacks@Goutham MINGW64 ~/OneDrive/Desktop/DevOps/Kubernetes/full-stack_chatApp/k8s (main)
$ kubectl apply -f namespace.yml
namespace/chat-app created

jacks@Goutham MINGW64 ~/OneDrive/Desktop/DevOps/Kubernetes/full-stack_chatApp/k8s (main)
$ kubectl get ns
NAME                   STATUS   AGE
chat-app               Active   11s
default                Active   184d
ingress-nginx          Active   184d
kube-node-lease        Active   184d
kube-public            Active   184d
kube-system            Active   184d
kubernetes-dashboard   Active   183d
```

- Create deployments for backend,frontend and mongodb

```bash
jacks@Goutham MINGW64 ~/OneDrive/Desktop/DevOps/Kubernetes/full-stack_chatApp/k8s (main)$ kubectl apply -f backend-deployment.yml -n chat-app
deployment.apps/backend-deployment created
jacks@Goutham MINGW64 ~/OneDrive/Desktop/DevOps/Kubernetes/full-stack_chatApp/k8s (main)$ kubectl apply -f secrets.yml -n chat-app
NAME                                  READY   STATUS    RESTARTS   AGE
backend-deployment-7b7d7b4c9f-cqnx8   1/1     Running   0          7m26s
mongodb-deployment-c7d774f8f-lr54j    1/1     Running   0          20m

```

- Create services for backend,frontend and mongodb

```bash
jacks@Goutham MINGW64 ~/OneDrive/Desktop/DevOps/Kubernetes/full-stack_chatApp/k8s (main)
$ kubectl apply -f backend-service.yml -n chat-app
service/backend created
jacks@Goutham MINGW64 ~/OneDrive/Desktop/DevOps/Kubernetes/full-stack_chatApp/k8s (main)
$ kubectl apply -f frontend-service.yml -n chat-app
service/frontend created

jacks@Goutham MINGW64 ~/OneDrive/Desktop/DevOps/Kubernetes/full-stack_chatApp/k8s (main)
$ kubectl apply -f mongodb-service.yml -n chat-app
service/mongodb created

jacks@Goutham MINGW64 ~/OneDrive/Desktop/DevOps/Kubernetes/full-stack_chatApp/k8s (main)
$ kubectl get svc -n chat-app
NAME       TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)     AGE
backend    ClusterIP   10.98.24.182     <none>        5001/TCP    5m49s
frontend   ClusterIP   10.100.132.235   <none>        80/TCP      3m40s
mongodb    ClusterIP   10.108.117.50    <none>        27017/TCP   2m55s
```

- Port forwarding

```bash
jacks@Goutham MINGW64 ~/OneDrive/Desktop/DevOps/Kubernetes/full-stack_chatApp/k8s (main)
$ kubectl port-forward service/frontend -n chat-app 80:80
Forwarding from 127.0.0.1:80 -> 80
Forwarding from [::1]:80 -> 80


jacks@Goutham MINGW64 ~/OneDrive/Desktop/DevOps/Kubernetes/full-stack_chatApp/k8s (main)
$ kubectl port-forward service/frontend -n chat-app 80:80 &
[2] 1160
Forwarding from 127.0.0.1:80 -> 80
Forwarding from [::1]:80 -> 80

jacks@Goutham MINGW64 ~/OneDrive/Desktop/DevOps/Kubernetes/full-stack_chatApp/k8s (main)
$
```

- Create ingress

```bash
jacks@Goutham MINGW64 ~/OneDrive/Desktop/DevOps/Kubernetes/full-stack_chatApp/k8s (main)
$ kubectl apply -f ingress.yml -n chat-app
ingress.networking.k8s.io/chatapp-ingress created
jacks@Goutham MINGW64 ~/OneDrive/Desktop/DevOps/Kubernetes/full-stack_chatApp/k8s (main)
$ kubectl get ns
NAME                   STATUS   AGE
chat-app               Active   3h27m
default                Active   184d
ingress-nginx          Active   184d
kube-node-lease        Active   184d
kube-public            Active   184d
kube-system            Active   184d
kubernetes-dashboard   Active   183d

```
