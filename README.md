rpi-hdmi-webcam
============================

Set up a Raspberry Pi in combination with a Raspberry Pi camera to act as a HDMI webcam.

Thanks to https://medium.com/javarevisited/using-a-raspberry-pi-as-hdmi-camera-92af84aafee2 for the idea.

Requirements
------------

An installed Raspberry Pi with a Raspberry Pi camera attached to it.

I used
* a Raspberry Pi Zero 2 W: https://www.berrybase.de/raspberry-pi/raspberry-pi-computer/boards/raspberry-pi-zero-2-w?c=319
* a Raspberry Pi High Quality camera: https://www.berrybase.de/raspberry-pi/raspberry-pi-computer/kameras/raspberry-pi-high-quality-kamera?c=341
  plus a wide-angle lens: https://www.berrybase.de/raspberry-pi/raspberry-pi-computer/kameras/6mm-weitwinkelobjektiv-cs-mount?c=341
* a camera mount: https://www.berrybase.de/raspberry-pi/raspberry-pi-computer/gehaeuse/gehaeuse-halter-fuer-kameramodul/pro-mounting-plate-f-252-r-high-quality-camera-und-raspberry-pi-zero?c=329
* connector cable: https://www.berrybase.de/raspberry-pi/raspberry-pi-computer/kabel-adapter/gpio-csi-dsi-kabel/flexkabel-f-252-r-raspberry-pi-zero-und-kameramodul?number=RPIZ-FLEX-15
* an old 4GB micro SD card
* a gooseneck with table clamp: https://www.berrybase.de/neu/flexibles-schwanenhals-stativ-mit-tischklemme-40cm-schwarz?c=2407
* a Mini-HDMI to HDMI cable

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
