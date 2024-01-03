# k3s
kubernetes playground 


1. Install K3s single-node cluster  
```
sudo curl -sfL https://get.k3s.io | sh -
```
2. Install ***kubestl***
```
sudo curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/arm64/kubectl"
sudo mv kubectl /usr/local/bin
sudo chmod +x /usr/local/bin/kubectl
```
3. Copy k3s config to ~/.kube/config

```
sudo cp /etc/rancher/k3s/k3s.yaml ~/.kube/config
chown $(id -u):$(id -g) ~/.kube/config
```
4. Check kubernetes cluster

- kubectl cluster-info
```
Kubernetes control plane is running at https://127.0.0.1:6443
CoreDNS is running at https://127.0.0.1:6443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
Metrics-server is running at https://127.0.0.1:6443/api/v1/namespaces/kube-system/services/https:metrics-server:https/proxy
```

# Deploy simple app

```
kubectl apply -f ~/k3s/whoami/whoami.yml
```

1. Check pods 
- kubectl -n k3s-test get pods
```
NAME                            READY   STATUS    RESTARTS       AGE
whoami-deploy-8f655c8cd-hslkz   1/1     Running   1 (134m ago)   16h
whoami-deploy-8f655c8cd-z5wx4   1/1     Running   1 (134m ago)   16h
whoami-deploy-8f655c8cd-8vkkp   1/1     Running   1 (134m ago)   16h
```
2. Get external ip 

```
- curl ifconfig.io
```

3. Check applications 
```
curl <external_ip\test>
Hostname: whoami-deploy-8f655c8cd-z5wx4
IP: 127.0.0.1
IP: ::1
IP: 10.42.0.31
IP: fe80::8c63:45ff:fe70:f179
RemoteAddr: 10.42.0.28:37526
GET /test HTTP/1.1
Host: <external_ip>
User-Agent: curl/7.81.0
Accept: */*
Accept-Encoding: gzip
X-Forwarded-For: 10.42.0.1
X-Forwarded-Host: <external_ip>
X-Forwarded-Port: 80
X-Forwarded-Proto: http
X-Forwarded-Server: traefik-f4564c4f4-vv95n
X-Real-Ip: 10.42.0.1

```