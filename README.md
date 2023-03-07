# minio-cluster-deployment-ubuntu
Example deployment of a Min.io cluster on 2 Ubuntu nodes using Ansible.

## Testbed
The testbed is composed of two Ubuntu 22.04.1 server nodes. 

Run the testbed:
```bash
# @/testbed
vagrant up
```

Stop and remove the testbed:
```bash
# @/testbed
vagrant destroy -f
```

## Deployment
Steps to deploy the Minio object storage cluster:
1. Ensure DNS config:
   
   Chage the `playbooks/templates/cluster_dns` template to your desired DNS names, then run the playbook:
   ```bash
   ansible-playbook playbooks/1_setup_dns.yml \
        -i inventory/minio1 \
        -i inventory/minio2
   ```
2. Show disks:
   ```bash
   ansible-playbook playbooks/2_show_disks.yml \
        -i inventory/minio1 \
        -i inventory/minio2
   ```

3. Setup disks for Minio:
   ```bash
   ansible-playbook playbooks/3_setup_disks.yml \
        -i inventory/minio1 \
        -i inventory/minio2 \
        -e "DISKS=sdc,sdd"
   ```

4. Ensure Minio is installd and configured:
    
    Chage the `playbooks/templates/minio_conf` template to your desired configuration, then run the playbook:
    ```bash
   ansible-playbook playbooks/4_ensure_minio.yml \
        -i inventory/minio1 \
        -i inventory/minio2
   ```