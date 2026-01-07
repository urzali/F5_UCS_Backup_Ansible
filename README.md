# F5_UCS_Backup_Ansible
Ansible script to backup UCS files using encrypted username and password

The script requires following items to be pre configured

1- Install F5 module on Ansible with below command:
ansible-galaxy collection install f5networks.f5\_modules


ls -l /root/.ansible/collections/ansible_collections/f5networks/f5_modules
(https://clouddocs.f5.com/products/orchestration/ansible/devel/usage/getting_started.html)

2- Save your password in a file and encrypt it

a- Create a file and add your password there:
/
vi bigip_pass
…
Secret password: “enteryourpasswordhere”
/

b- Run below command in terminal:

ansible-vault encrypt bigip_pass
New Vault Password: 
Confirm New Vault password:

Now if you cat bigip_pass, you will see encrypted file

If you want to see the password within this file in your playbook, you have 3 options: 

i- Run your playbook and have prompted for the password. 
ansible-playbook vault-test.yml --ask-vault-pass

ii- Store the vault password in file and tell ansible where that file is
ansible-playbook vault-test.yml --vault-password-file /variable_files/vault.pass.txt

make sure you save the vault.pass.txt with proper creds access so no one else can open it.

iii- Specify the location of a password file in ansible.cfg

vault_password_file = /variable_files/vault-pass.txt


Decrypt file: ansible-vault decrypt bigip_pass // will prompt you to put vault password
Rekey: ansible-vault rekey bigip_pass 


In the playbook, mention the password as such:

Secret password: { { password } }

// Secret password is the variable where the password is stored

Mention the vault file that has password within playbook as "  vars_files: bigip_pass"

It’s a good idea to use no_log on any task that interacts with sensitive data. You should also be aware of its limitations: It will not prevent logging if Ansible debugging is turned on.

3- Modify hosts file with remote nodes



Command to run to take backups: ansible-playbook /home/ansible/BIGIP/bigip_backup.yml -i /home/ansible/BIGIP/variable_files/hosts --vault-password-file /home/ansible/BIGIP/variable_files/.vault.pass.txt
