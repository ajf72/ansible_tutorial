# ansible_tutorial

Ansible Lab Backup

> Adjust the Ansible CFG
> location ansible-csr1000v directory
> add the foolowing
> config file for ansible-csr1000v

[defaults]

## Use local hosts file in this folder
```
inventory=./hosts
host_key_checking = False # Don't worry about RSA Fingerprints
retry_files_enabled = False # Do not create them
deprecation_warnings = False # Do not show warnings
```

> Create an Ansible Playbook
  location ansible-csr1000v directory
  name backup_cisco_router_playbook.yaml
  the following code has been add

```yaml
---
- name: AUTOMATIC BACKUP OF RUNNING-CONFIG
  hosts: CSR1kv
  gather_facts: false
  connection: local
  tasks:
   - name: DISPLAYING THE RUNNING-CONFIG
     ios_command:
      commands:
       - show running-config
     register: config
   - name: SAVE OUTPUT TO ./backups/
     copy:
      content: "{{ config.stdout[0] }}"
      dest: "backups/show_run_{{ inventory_hostname }}.txt"
```

## Run the Ansible backup Playbook.

