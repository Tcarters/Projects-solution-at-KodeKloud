
## Tasks:


a. Create an ini type Ansible inventory file /home/thor/playbook/inventory on jump host.

b. Add App Server 1 in this inventory along with required variables that are needed to make it work.

c. The inventory hostname of the host should be the server name as per the wiki, for example stapp01 for app server 1 in Stratos DC.

Note: Validation will try to run the playbook using command ansible-playbook -i inventory playbook.yml so please make sure the playbook works this way without passing any extra arguments.



## Solution

### Step 1: Setup Inventory File
- Config File `ansible.cfg`:

```cfg
[defaults]
host_key_checking = False
```

- cat inventory file:

```yaml 
[all]

stapp01 ansible_host=172.16.238.10 ansible_user=tony ansible_ssh_pass=Ir0nM@n ansible_ssh_common_args='-o StrictHostKeyChecking=no'

```

- Test by ping:

```bash
    ansible all -i inventory -m ping
```

![image](https://github.com/Tcarters/Projects-solution-at-KodeKloud/assets/71230412/b0ab3d8c-eb5e-41ff-bd4b-f03e386727e4)


### Step 2: Run Playbook

```yaml
---
- hosts: all
  become: yes
  become_user: root
  tasks:
    - name: Install httpd package    
      yum: 
        name: httpd 
        state: installed
    
    - name: Start service httpd
      service:
        name: httpd
        state: started
```

- Output

![image](https://github.com/Tcarters/Projects-solution-at-KodeKloud/assets/71230412/d3d5a0bb-96c2-4e1d-aa3d-7876e05ad21d)

