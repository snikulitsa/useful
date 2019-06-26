# Kubernetes (LinuxMint 19.1 | Ubuntu 18.04)
#### Installation
First Install [DOCKER](DOCKER.md)  
Kubernetes installation:  
```bash
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add
sudo apt-add-repository "deb http://apt.kubernetes.io/ kubernetes-xenial main"
sudo apt-get update
sudo apt install -y kubeadm
sudo swapoff -a
```
Delete swap row from
```bash
sudo mcedit /etc/fstab
```
```bash
sudo kubeadm init --pod-network-cidr=192.168.88.0/24 # This is virtual Network
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
sudo kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
kubectl get pods --all-namespaces
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/master/aio/deploy/recommended/kubernetes-dashboard.yaml
```
#### Dashboard installation
Create file  
```bash
nano dashboard-adminuser.yaml
```
Add to file:
```yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: admin-user
  namespace: kube-system
```
Then run  
```bash
kubectl apply -f dashboard-adminuser.yaml
```
Create file
```bash
nano configure-admin-user-access.yaml
```
Add to file:
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: admin-user
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: cluster-admin
subjects:
- kind: ServiceAccount
  name: admin-user
  namespace: kube-system
```
Then run  
```bash
kubectl apply -f configure-admin-user-access.yaml
# Get TOKEN
kubectl -n kube-system describe secret $(kubectl -n kube-system get secret | grep admin-user | awk '{print $1}')
```
Run proxy  
```bash
kubectl proxy
```
`Kubectl` will make `Dashboard` available at `http://localhost:8001/api/v1/namespaces/kube-system/services/https:kubernetes-dashboard:/proxy/`  
To allow remote access for `Dashboard` from remote hosts run `proxy` as follow:
```bash
# TODO: configure HTTPS first
kubectl proxy --address='HOST_IP' --accept-hosts='^*$' --accept-paths='^*$'
```
Remote access can only be accessed via `HTTPS`
