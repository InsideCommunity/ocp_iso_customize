# ocp_iso_customize

## Description

Ansible role to generate Red Hat CoreOS or Fedora CoreOS live iso with network,partitioning and ignition configured to speedup Openshift cluster bootstraping.

# Usage

Overwrite vars defined in defaults to fit your needs.

Create playbook:

```
cat << EOF >> iso_playbook.yml
---
- name: Manage Openshift Images
  hosts: localhost
  become: true
  roles:
    - role: ocp_iso_customize
EOF
```

Execute:

```
ansible-playbook -i inventory iso_playbook.yml
```