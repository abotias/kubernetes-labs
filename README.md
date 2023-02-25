# kubernetes-labs


## INSTALL

### Install kubectl

```sh
sudo apt-get install -y ca-certificates curl

sudo curl -fsSLo /etc/apt/keyrings/kubernetes-archive-keyring.gpg https://packages.cloud.google.com/apt/doc/apt-key.gpg

echo "deb [signed-by=/etc/apt/keyrings/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list

sudo apt-get update

sudo apt-get install -y kubectl
```

### Download and install config

```sh
mkdir -p ~/.kube
mv 0293120-kubeconfig.yaml ~/.kube/config
```

### Check connection

```sh
kubectl get nodes
```


## MGMT

### Namespaces

```sh
kubectl apply -f 00-namespace.yaml
```

```bash
adrian@ADRIANLT:~/kubernetes-labs/wordpress$ kubectl get ns
NAME              STATUS   AGE
default           Active   24m
kube-node-lease   Active   24m
kube-public       Active   24m
kube-system       Active   24m
testing           Active   14s
```

### Services

```sh
kubectl -n testing apply -f 01-wordpress-service.yaml
```

```bash
adrian@ADRIANLT:~/kubernetes-labs/wordpress$ kubectl -n testing get svc
NAME        TYPE       CLUSTER-IP     EXTERNAL-IP   PORT(S)        AGE
wordpress   NodePort   10.245.6.175   <none>        80:31000/TCP   95s
```

## Delete service

```sh
kubectl -n testing delete svc wordpress
```

### Replication Controller

```sh
kubectl -n testing apply -f 02-wordpress-rc.yaml
```

```bash
adrian@ADRIANLT:~/kubernetes-labs/wordpress$ kubectl -n testing get pods
NAME              READY   STATUS    RESTARTS   AGE
wordpress-lltlm   1/1     Running   0          56s
```

### Delete pod

```sh
kubectl -n testing delete pod wordpress-lltlm
```


## Access

Show public IP

```bash
adrian@ADRIANLT:~/kubernetes-labs/wordpress$ kubectl get nodes -o wide
NAME                   STATUS   ROLES    AGE   VERSION   INTERNAL-IP   EXTERNAL-IP
pool-nhlgkdq75-qr00s   Ready    <none>   49m   v1.25.4   10.110.0.2    X.X.X.X
```
