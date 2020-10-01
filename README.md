# slate-ansible
Registers an existing Kubernetes cluster with SLATE.

## Requirements
- User with `ssh` access to `node1` and read access to `/etc/kubernetes/admin.conf`.
- `kubectl` installed on `node1`.
- Kubernetes cluster instantiated with MetalLB.

## Inventory File Format
This playbook is designed to work with inventory files formatted to be used with kubespray. As such, your inventory file, at a minimum, should look like the following:
```
all:
  children:
    k8s-cluster:
      children:
        kube-master:
      vars:
        slate_cli_token: SLATE_TOKEN
        slate_cli_endpoint: https://api.slateci.io:443
        slate_group_name: SLATE_GROUP_NAME
        slate_org_name: SLATE_ORG_NAME
        slate_cluster_name: SLATE_CLUSTER_NAME
    kube-master:
      hosts:
        node1:
  hosts:
    node1:
      ansible_host: IP_ADDRESS
```

If you used kubespray to provision your Kubernetes cluster, you can use the same `hosts.yaml` file you used with kubespray.

## Use
`ansible-playbook -i INVENTORY_FILE -u SSH_USER site.yml`
