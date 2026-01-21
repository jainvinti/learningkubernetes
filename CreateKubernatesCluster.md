### 1 Set host name
```
hostnamectl set-hostname node10.dockerhunt.com
```

### 2 Update yum
```
sudo yum check-update
```

### 3 Configure firewall
```
firewall-cmd --permanent --add-port=6443/tcp
firewall-cmd --permanent --add-port=2379-2380/tcp
firewall-cmd --permanent --add-port=10250/tcp
firewall-cmd --permanent --add-port=10251/tcp
firewall-cmd --permanent --add-port=10252/tcp
firewall-cmd --permanent --add-port=10255/tcp
firewall-cmd --reload
```

### 4 IP Tables
```
cat <<EOF > /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
EOF
sysctl --system
```

### 5 Disable SELinux
```
setenforce 0
sed -i 's/^SELINUX=enforcing$/SELINUX=permissive/' /etc/selinux/config
```

### 6 Turn off swap
```
sed -i '/swap/s/^/#/' /etc/fstab
swapoff -a
```

### 7 Install Docker
```
sudo yum install -y yum-utils device-mapper-persistent-data lvm2
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
yum list docker-ce --showduplicates | sort -r
sudo yum install docker-ce-18.06.3.ce
systemctl enable docker && systemctl start docker
```

### 8 Add repository
```
cat <<EOF > /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-\$basearch
enabled=1
gpgcheck=1
repo_gpgcheck=1
gpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg
exclude=kubelet kubeadm kubectl
EOF
```

### 9 Install Kubernetes
```
yum install -y kubelet kubeadm kubectl --disableexcludes=kubernetes
systemctl enable kubelet
```

### 10 Initialize the k8s master
```
kubeadm init --pod-network-cidr=192.168.0.0/16 --apiserver-advertise-address=<ip_of_machine_eth0>
kubeadm init --pod-network-cidr=192.168.0.0/16 --apiserver-advertise-address=10.74.130.21(eth0)
```

### 11 Configure kubectl
```
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

### 12 Install the Virtual Network layer
```
kubectl apply -f https://docs.projectcalico.org/v3.11/manifests/calico.yaml
```

### 13 Join Worker node
```
kubeadm join <ip_of_machine_eth0>:6443 --token <token> --discovery-token-ca-cert-hash <hash>
kubeadm join 10.74.130.21:6443 --token nrdq2n.oircm4039x0n5mro     --discovery-token-ca-cert-hash sha256:1a6ec438decf184f4fe1ef262d6d61ad4d9a7492ca537d3bbc6dd7c3bf51ce43
```

### Commands
```kubectl get nodes
kubectl get pods -n kube-system

Hello world 
kubectl run nginx --image=nginx:1.10.0 --requests=cpu=200m --replicas=2
kubectl get pods -o wide
```
