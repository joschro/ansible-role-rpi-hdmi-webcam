rpi-hdmi-webcam
============================

Set up a Raspberry Pi in combination with a Raspberry Pi camera to act as a HDMI webcam

Requirements
------------

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required.

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

```
---
# Ansible Playbook to set up a Raspberry Pi with Raspberry camera as HDMI webcam
- name: Set up a Raspberry Pi HDMI webcam
  hosts: localhost
  gather_facts: no
  roles:
    - { role: joschro.rpi-hdmi-webcam }
```
Create a requirements.yml file in the same directory:
```
# Install a role from the Ansible Galaxy
#- src: joschro.rpi-hdmi-webcam

# Install a role from GitHub
- name: joschro.rpi-hdmi-webcam
  src: https://github.com/joschro/ansible-role-rpi-hdmi-webcam
```

You can now run the two commands on the command line to run the installation:
```
ansible-galaxy install -r requirements.yml --force
ansible-playbook -i localhost ansible-playbook-rpi-hdmi-webcam.yml

License
-------

GPLv3

Author Information
------------------

joschro
