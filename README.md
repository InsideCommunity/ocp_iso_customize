# insidegroup.ocp_iso_customize

[![Maintainer](https://img.shields.io/badge/maintained%20by-InsideCommunity-00548c?style=flat-square)](https://github.com/InsideCommunity)
[![License](https://img.shields.io/github/license/InsideCommunity/ocp_iso_customize?style=flat-square)](https://github.com/InsideCommunity/ocp_iso_customize/blob/main/LICENSE)
[![Release](https://img.shields.io/github/v/release/InsideCommunity/ocp_iso_customize?style=flat-square)](https://github.com/InsideCommunity/ocp_iso_customize/releases)
[![Status](https://img.shields.io/github/workflow/status/InsideCommunity/ocp_iso_customize/Ansible%20Molecule?style=flat-square&label=tests)](https://github.com/InsideCommunity/ocp_iso_customize/actions?query=workflow%3A%22Ansible+Molecule%22)
[![Ansible Galaxy](https://img.shields.io/badge/ansible-galaxy-black.svg?style=flat-square&logo=ansible)](https://galaxy.ansible.com/insidegroup/ocp_iso_customize)[![Ansible version](https://img.shields.io/badge/ansible-%3E%3D2.9-black.svg?style=flat-square&logo=ansible)](https://github.com/ansible/ansible)

⭐ Star us on GitHub — it motivates us a lot!

Role to manage automatic rhcoreos or coreos creation with kargs and livekargs for Openshift/OKD installations.
It has been made to iterate over inventory using bootstrap, masters and workers groups


**Platforms Supported**:

| Platform | Versions |
|----------|----------|
| Ubuntu | focal, jammy |
| Fedora | all |

## ⚠️ Requirements

Ansible >= 2.9.

Due to coreos-installer usage:
* [openssl1.1-1.1](https://download-ib01.fedoraproject.org/pub/fedora/linux/releases/37/Everything/x86_64/os/Packages/o/openssl1.1-1.1.1q-2.fc37.x86_64.rpm) (for Fedora)
* [libssl1.1](http://nz2.archive.ubuntu.com/ubuntu/pool/main/o/openssl/libssl1.1_1.1.1f-1ubuntu2.17_amd64.deb) (for Ubuntu)

### Ansible role dependencies

None.

## ⚡ Installation

### Install with Ansible Galaxy

```shell
ansible-galaxy install insidegroup.ocp_iso_customize
```

### Install with git

If you do not want a global installation, clone it into your `roles_path`.

```bash
git clone https://github.com/InsideCommunity/ocp_iso_customize.git  insidegroup.ocp_iso_customize
```

But I often add it as a submodule in a given `playbook_dir` repository.

```bash
git submodule add https://github.com/InsideCommunity/ocp_iso_customize.git roles/insidegroup.ocp_iso_customize
```

As the role is not managed by Ansible Galaxy, you do not have to specify the
github user account.

### ✏️ Example Playbook

Basic usage is:

```yaml
- hosts: all
  roles:
    - role: insidegroup.ocp_iso_customize
      vars:
        ocp_iso_customize_coreos_img_url: ''
        ocp_iso_customize_coreos_installer_type: podman
        ocp_iso_customize_coreos_installer_url: http://mirror.openshift.com/pub/openshift-v4/x86_64/clients/coreos-installer/latest/coreos-installer
        ocp_iso_customize_dest: /var/www/html/example/images/coreOS
        ocp_iso_customize_dest_device: sda
        ocp_iso_customize_domain: example.com
        ocp_iso_customize_extra_live_karg: ''
        ocp_iso_customize_filer: http://file.example.com/ocp4
        ocp_iso_customize_filer_ignition_path: '{{ ocp_iso_customize_filer }}/example/'
        ocp_iso_customize_kargs: {}
        ocp_iso_customize_output_type: minimal
        ocp_iso_customize_primary_dns: 10.0.10.250
        ocp_iso_customize_role: worker
        ocp_iso_customize_secondary_dns: 8.8.8.8
        ocp_iso_customize_source_iso_url: https://builds.coreos.fedoraproject.org/prod/streams/stable/builds/37.20230122.3.0/x86_64/fedora-coreos-37.20230122.3.0-live.x86_64.iso
        ocp_iso_insecure_ignition: true
        
```

## ⚙️ Role Variables

Variables are divided in three types.

The **default vars** section shows you which variables you may
override in your ansible inventory. As a matter of fact, all variables should
be defined there for explicitness, ease of documentation as well as overall
role manageability.

The **context variables** are shown in section below hint you
on how runtime context may affects role execution.

### Default variables
Role default variables from `defaults/main.yml`.

| Variable Name | Value |
|---------------|-------|
| ocp_iso_customize_source_iso_url | https://builds.coreos.fedoraproject.org/prod/streams/stable/builds/37.20230122.3.0/x86_64/fedora-coreos-37.20230122.3.0-live.x86_64.iso |
| ocp_iso_customize_coreos_img_url |  |
| ocp_iso_customize_coreos_installer_type | podman |
| ocp_iso_customize_output_type | minimal |
| ocp_iso_customize_coreos_installer_url | http://mirror.openshift.com/pub/openshift-v4/x86_64/clients/coreos-installer/latest/coreos-installer |
| ocp_iso_insecure_ignition | True |
| ocp_iso_customize_domain | example.com |
| ocp_iso_customize_primary_dns | 10.0.10.250 |
| ocp_iso_customize_secondary_dns | 8.8.8.8 |
| ocp_iso_customize_filer | http://file.example.com/ocp4 |
| ocp_iso_customize_filer_ignition_path | {{ ocp_iso_customize_filer }}/example/ |
| ocp_iso_customize_dest | /var/www/html/example/images/coreOS |
| ocp_iso_customize_role | worker |
| ocp_iso_customize_kargs | {}<br> |
| ocp_iso_customize_dest_device | sda |
| ocp_iso_customize_extra_live_karg |  |

Focus on **ocp_iso_customize_kargs** if you needed to customize networking
```yaml
# Should be defined in host_vars both group_vars and host_vars
ocp_iso_customize_kargs:
  client_ip: 10.0.10.10
  gw_ip: 10.0.10.254
  netmask: 255.255.255.0
  interface: bond0
  autoconf: none
  bond:
    - name: bond0
      ifaces: ens18,ens19
      bond_opts: mode=active-backup,fail_over_mac=follow
  disabled_interfaces:
    - eno1
    - eno2
```

### Context variables

None.

## ©️ [License](LICENSE)

## 📄 [CHANGELOG.md](CHANGELOG.md)

## Author Information

Inside Group

## 👏 Special thanks

README generated with [ansible-gendoc](https://github.com/claranet/ansible-gendoc)