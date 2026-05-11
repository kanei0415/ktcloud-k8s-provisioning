### Vagrant
```terminal
vagrant up --provider vmware_desktop
```
```terminal
vagrant destroy -f
```
```terminal
vagrant ssh-config > ~/.ssh/config
```
```terminal
vagrant halt

vagrant provision

vagrant status
```

### Ansible
```terminal
ansible all -i ansible/inventory.ini -m ping
```
```terminal
ansible-playbook -i ansible/inventory.ini ansible/main.yaml
```

### Calico
```terminal
curl -L https://github.com/projectcalico/calico/releases/download/v3.27.3/calicoctl-linux-arm64 -o calicoctl
chmod +x calicoctl
sudo mv calicoctl /usr/local/bin/
calicoctl version
```

```terminal
echo 'export DATASTORE_TYPE=kubernetes' >> ~/.bashrc
echo 'export KUBECONFIG=~/.kube/config' >> ~/.bashrc
source ~/.bashrc
sudo ln -s /usr/local/bin/calicoctl /usr/bin/calicoctl
```

```terminal
[vagrant@k8s-master ~]$ sudo calicoctl node status
Calico process is running.

IPv4 BGP status
+-----------------+-------------------+-------+----------+-------------+
|  PEER ADDRESS   |     PEER TYPE     | STATE |  SINCE   |    INFO     |
+-----------------+-------------------+-------+----------+-------------+
| 192.168.241.145 | node-to-node mesh | up    | 01:27:23 | Established |
| 192.168.241.146 | node-to-node mesh | up    | 01:27:23 | Established |
| 192.168.241.147 | node-to-node mesh | up    | 01:27:23 | Established |
+-----------------+-------------------+-------+----------+-------------+

IPv6 BGP status
No IPv6 peers found.
```

### ArgoCD
```terminal
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath='{.data.password}' | base64 -d && echo
```
```terminal
kubectl delete ns argocd
kubectl get ns argocd -o json | jq '.spec.finalizers = []' | kubectl replace --raw "/api/v1/namespaces/argocd/finalize" -f -
```
```terminal
sudo curl -sSL -o /usr/local/bin/argocd https://github.com/argoproj/argo-cd/releases/latest/download/argocd-linux-amd64
sudo chmod +x /usr/local/bin/argocd
argocd version --client
```

### MasterNode
```terminal
vagrant ssh k8s-master
```

### Time Sync
```terminal
kubectl logs -n tigera-operator -l k8s-app=tigera-operato
```
```terminal
ansible-playbook -i ansible/inventory.ini ansible/time-sync.yaml
```
```terminal
kubectl delete pod -n tigera-operator -l k8s-app=tigera-operator
kubectl delete lease operator-lock -n tigera-operator
kubectl delete pod -n calico-system --all
```

### NFSProvisioner
```terminal
kubectl patch pv pv-nfs-provisioner-nfs-subdir-external-provisioner -p '{"metadata":{"finalizers":null}}' --type merge
```