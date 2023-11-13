
## Scenario

> There is data on jump host that needs to be copied on all application servers in Stratos DC. Nautilus DevOps team want to perform this task using Ansible. Perform the task as per details mentioned below:

## Mission

a. On jump host create an inventory file /home/thor/ansible/inventory and add all application servers as managed nodes.
b. On jump host create a playbook /home/thor/ansible/playbook.yml to copy /usr/src/data/index.html file to all application servers at location /opt/data.

Note: Validation will try to run the playbook using command ansible-playbook -i inventory playbook.yml so please make sure the playbook works this way without passing any extra arguments.


## Solution 

- `Inventory` file

```ini
stapp01 ansible_host=172.16.238.10 ansible_user=tony ansible_ssh_pass=Ir0nM@n ansible_ssh_common_args='-o StrictHostKeyChecking=no'

stapp02 ansible_host=172.16.238.11 ansible_user=steve ansible_ssh_pass=Am3ric@ ansible_ssh_common_args='-o StrictHostKeyChecking=no'

stapp03 ansible_host=172.16.238.12 ansible_user=banner ansible_ssh_pass=BigGr33n ansible_ssh_common_args='-o StrictHostKeyChecking=no'
```
- Test ping:
![image](https://github.com/Tcarters/Projects-solution-at-KodeKloud/assets/71230412/83d7ed33-ec6d-4aec-a364-aff0dd182e5c)


- Create Playbook file

```yaml
- name: Copy file to all servers
  hosts: all
  become: yes
  tasks:
  - name: Copy index file to /opt/devops
    copy:
      src: /usr/src/devops/index.html
      dest: /opt/devops
```

- Result

![image](https://github.com/Tcarters/Projects-solution-at-KodeKloud/assets/71230412/f95380f4-c558-424f-b6b7-3c0e82254e47)
