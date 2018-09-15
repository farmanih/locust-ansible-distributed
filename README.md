# Locust Ansible Distributed

### Run This Command Before Run Playbook For Setup Python on Remote Host
ansible locust-all -i hosts -u root -m raw -a 'DEBIAN_FRONTEND=noninteractive apt update && apt -y install python'

### Run Playbook For Deploying the Locust File and Installing Dependencies
ansible-playbook -i hosts locust.yaml

### Run This Command After All For Setup Master Node
ansible locust-master -i hosts -u root -m shell -a 'locust -f locustfile.py --master --host=https://example.com'

### Run This Command After All For Setup Slave Nodes
ansible locust-slaves -i hosts -u root -m shell -a 'locust -f locustfile.py --slave --master-host={{ MASTER_IP }}'
