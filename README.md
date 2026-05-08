### Vagrant
```terminal
vagrant up --provider vmware_desktop
```
```terminal
vagrant destroy -f
```
```terminal
vagrant ssh-config >> ~/.ssh/config
```

### Ansible
```terminal
ansible all -i ansible/inventory.ini -m ping
``
```terminal
ansible-playbook -i ansible/inventory.ini ansible/main.yaml
```

### ArgoCD
```terminal
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath='{.data.password}' | base64 -d
```