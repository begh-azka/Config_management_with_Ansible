# Config-Management-with-Ansible
Ansible Playbooks

### Commands:
```bash
# -m is to call the module
ansible -m ping [host-name/group]

# -a is the argument to the module
ansible -a uname [host-name/group]

# To run ansible playbooks
ansible-playbook [path-to-playbook]

# To pass variable value in command line
# Variable values passed using command line override values in playbooks or variable files
ansible-playbook -e [variable-value] [playbook.yml]
```

### Variables
- We can pass varaibles in command line or we can keep them in `group_vars` and `host_vars`.
- In group_vars, we can keep an all.yml file that contains variables that are common for all groups or we can keep individual var files for each group.
- If we need to define variables for each host, then host_vars should be used.
- Variable files for each group/host should have the same name as the group/host (eg., if group is ubuntu then its variables will be in ubuntu.yml in group_vars).
- We can also define variables in inventory and our playbooks.
- Command line variable values have the most precedence followed by playbooks, then host_vars and finally group_vars.
- If same variable is defined in group_vars and host_vars files, then host_vars will override the value in group_vars.

### Ansible Facts
- To print all the facts of vms
```
ansible -m setup all
```
- In playbooks, we can turn fact gathering to false. The default is True.
- To get value of certain facts, we can write ansible_distribution, ansible_hostname etc.
- To access a certain fact that is part of a dictionary - Example:
```json
"ansible_mounts": [
            {
                "block_available": 2030113,
                "block_size": 4096,
                "block_total": 2399739,
                "block_used": 369626,
                "device": "/dev/xvda4",
                "dump": 0,
                "fstype": "xfs",
                "inode_available": 4796432,
                "inode_total": 4832192,
                "inode_used": 35760,
                "mount": "/",
                "options": "rw,seclabel,relatime,attr2,inode64,logbufs=8,logbsize=32k,noquota",
                "passno": 0,
                "size_available": 8315342848,
                "size_total": 9829330944,
                "uuid": "497ad222-04fa-453f-b110-ba8001d38788"
            },
```
- We need to write **`ansible_mounts.block_available`** or **`ansible_mounts[block_available]`**. We are trying to get the value of the key.

### Dynamic Inventory for Cloud
- Install boto3 for this. `pip3 install boto3`
- This is recommended for Cloud
- For aws, all the files should end in aws_ec2.yml/yaml
- We need to use the ansible-inventory tool for this
  `ansible-inventory --list`
  `ansible-inventory --graph`
