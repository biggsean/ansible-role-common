Ansible Role: common v0.1
=========

Common role for securing and configuring servers.  This is currently only written for CentOS 7.x.

Requirements
------------

None

Role Variables
--------------

### common_yum_update_command
This defaults to 'default'.  The options can be found in the /etc/yum/yum-cron.conf

### common_fail2ban_template
Default template.  Overide it if you would like to use your own.

### common_fail2ban_destination
defaults to /etc/fail2ban/jail.d/00-common-role.local

### common_fail2ban_bantime
defaults to 3600

### common_fail2ban_banaction
defaults to 'iptables-multiport'

### common_iptables_template
default template.  overide if you would like to use your own.

### common_iptables_tcp_ports
list that defaults to [22].

### common_iptables_udp_ports
list that defaults to []

### common_root_password
when set will change the root password

### common_user_list
defaults to []
```
common_user_list:
  - username: foo
    groups:
    - bar
    key:  ssh_public_key
```

### common_sudoers_groups
defaults to []
```
common_sudoers_groups:
  - name: bar
    nopasswd: true
```
nopasswd is optional and defaults to false.

Dependencies
------------

None

Example Playbook
----------------

```
---
- hosts: all
  become: yes
  vars:
    - common_root_password: "{{ 'secure' | password_hash('sha512', 'MySalt') }}"
    - common_user_list:
      - username: foo
        groups:
        - bar
        key: https://github.com/foo.keys
    - common_sudoers_groups:
      - name: bar
        nopassword: true

  roles:
    - common
```

License
-------

BSD, MIT

