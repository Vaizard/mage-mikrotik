# mage-mikrotik

Ansible role to manage Mikrotik (RouterOS) APs from scratch.

## WARNING

Please note that due to the specifics of Mikrotik devices, this role assumes, that

```
mt_host_files: "host_files/{{ inventory_hostname }}"
mt_playbook_dir: "{{ playbook_dir }}"
```

are set. If you store your playbooks in /home/user/ansible, then this role will create within this path a subdirectory
`./host_files/{{ inventory_hostname }}`, where it will store certificate generations, that are to be used on the managed
device. Certs will be generated each time, but only when `mt_cert_regen` is set to `true`. Until certs are generated, the
www-ssl interface and the sstp vpn will not work. Since this role also tightens security on the managed device, the 
unencrypted www interface will be disabled, leaving you with only ssh access (until certs are generated and uploaded).
