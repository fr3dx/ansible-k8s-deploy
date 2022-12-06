# Ansible playbook - Install Kubernetes Cluster on Ubuntu 22.04

> Requirements:

```
OS version Ubuntu 22.04
Minimum 2GB RAM or more
Minimum 2 CPU cores / or 2 vCPU
20 GB free disk space on /var or more
Deployed SSH keys on hosts
```

> Environment (virtualbox):

```
Master Node: 192.168.99.50   k8smaster.example.net k8smaster (bridged and nat network, acts as gw)
Worker Node: 10.0.2.51   k8sworker1.example.net k8sworker1 (nat network)
Worker Node: 10.0.2.52   k8sworker2.example.net k8sworker2 (nat network)
```

> Useful commands:

```
### Ensure all hosts are available

ansible all -m ping --ask-vault-pass --extra-vars '@passwd.yml'

### Run playbook:

- ansible-playbook site.yml -i inventory --ask-vault-pass --extra-vars '@passwd.yml'

### Ansible vault

Create / edit encrypted pwd file:

- ansible-vault create passwd.yml
- ansible-vault edit passwd.yml

### Pods statuses in groups calico-node and calico-kube-controllers (jq should be installed in case manual test)

- kubectl get pods -l k8s-app=calico-node -n kube-system -o json | jq ".items[].status.phase" | uniq

- kubectl get pods -l k8s-app=calico-kube-controllers -n kube-system -o json | jq ".items[].status.phase" | uniq
```