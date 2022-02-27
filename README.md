rpi-hdmi-webcam
============================

Set up a Raspberry Pi in combination with a Raspberry Pi camera to act as a HDMI webcam

Requirements
------------

An installed Raspberry Pi with a Raspberry Pi camera attached to it.

Dependencies
------------

Needs Ansible role joschro.rpi-hdmi-webcam from Ansible Galaxy 

Example Playbook
----------------

```
---
# Ansible Playbook to set up a Raspberry Pi with Raspberry camera as HDMI webcam
- name: Set up a Raspberry Pi HDMI webcam
  hosts: localhost
  gather_facts: no
  tasks:
    - name: Make sure that an empty requirements.yml file exists
      file:
        path: requirements.yml
        state: touch

    - name: Create requirements.yml
      blockinfile:
        path: requirements.yml
        create: yes
        block: |
          # Install a role from the Ansible Galaxy
          #- src: joschro.rpi-hdmi-webcam
          
          # Install a role from GitHub
          - src: https://github.com/joschro/ansible-role-rpi-hdmi-webcam
            name: joschro.rpi-hdmi-webcam

    - name: Install required packages
      become: yes
      package:
        name: git
        state: present

    - name: Source required roles
      command: ansible-galaxy install -r requirements.yml --force

    - name: Execute role
      include_role:
        name: joschro.rpi-hdmi-webcam
```

You can now run the following commands on the command line to start the installation:
```
sudo apt update
sudo apt install ansible

ansible-playbook -i localhost ansible-playbook-rpi-hdmi-webcam.yml
```

License
-------

GPLv3

Author Information
------------------

joschro
