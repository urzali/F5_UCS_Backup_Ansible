# F5_UCS_Backup_Ansible
Ansible script to backup UCS files using encrypted username and password

The script requires following items to be pre configured

1- Install F5 module on Ansible with below command:
ansible-galaxy collection install f5networks.f5\_modules

ls -l /root/.ansible/collections/ansible_collections/f5networks/f5_modules
(https://clouddocs.f5.com/products/orchestration/ansible/devel/usage/getting_started.html)


Command to run to take backups: ansible-playbook /home/ansible/BIGIP/bigip_backup.yml -i /home/ansible/BIGIP/hosts --vault-password-file /home/ansible/BIGIP/.vault.pass.txt
