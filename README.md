# Locust Ansible Distributed
Locust is an easy-to-use, distributed, user load testing tool. It is intended for load-testing web sites (or other systems) and figuring out how many concurrent users a system can handle.
With this repo you can run locust automatically with ansible without any dependency on cloud servers or fresh remote hosts in master slave (distributed) mode.

## Step 1
Edit the hosts file and add yor hosts on this file make your locust file.

## Step 2
Run the following commands with replace the host site and master server ip

### Run This Command Before Run Playbook For Setup Python on Remote Host
ansible locust-all -i hosts -u root -m raw -a 'DEBIAN_FRONTEND=noninteractive apt update && apt -y install python'
### Run Playbook For Deploying the Locust File and Installing Dependencies
ansible-playbook -i hosts locust.yaml
### Run This Command After All For Setup Master Node
ansible locust-master -i hosts -u root -m shell -a 'locust -f locustfile.py --master --host=https://example.com'
### Run This Command After All For Setup Slave Nodes
ansible locust-slaves -i hosts -u root -m shell -a 'locust -f locustfile.py --slave --master-host={{ MASTER_IP }}'
