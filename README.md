# mage-mikrotik

A somewhat unusual Ansible Mikrotik role. Until there's a propper Mikrotik connector, this role will generate a bash script and relevant (helper) files in {{ mikrotik_script_path }}. 
These are then to be executed manually.

Example playbook

```
---
- hosts: localhost
  vars:
    mikrotik_script_wipe: true
    mikrotik_script_path: ~/mikrotik-run
    mt_vpn_provider_service: sstp
    mt_vpn_provider_profile: default
    mikrotik:
       - ssh_host: gw01.example.com
         ssh_user: admin
         ssh_pass: mysecretpass
         ssh_port: 22
             vpn_sstp:
            certpass: 96EazNUJwwNuq2Kkzbk7ihMdAR0rzxWQoYcdDJ0YPvk
            certbits: 8192
            certsubj: "/C=CZ/O=Example Inc./CN=gw01.example.com"
         vpn_user:
            - user: my_vpn_name
              pass: AFQnWlL51Kp55+96afcNnVZPKPga5OSw1rfl39B1t0U
              service: sstp
              profile: sstp-admin
         ssh_keys:
            - user: admin
              src: ~/.ssh/id_rsa.pub
              dest: my_key_rsa.pub
       - ssh_host: gw02.example.com
         ssh_user: admin
         ssh_pass: myothersecretpass
  roles:
    - { role: make-mikrotik }
 ```
 
 