# ansible-role-fortiadc-server-load-balance

## Description

Ansible role to create/update Fortinet's FortiADC SLB entries using REST API. Is the "complete edition" that makes use the following roles:
- [ndkprd.fad_slb_real_server](https://github.com/ansible-role-fad-slb-real-server)
- [ndkprd.fad_slb_real_server_pool](https://github.com/ansible-role-fad-slb-real-server-pool)
- [ndkprd.fad_slb_content_routing](https://github.com/ansible-role-fad-slb-content-routing)
- [ndkprd.fad_slb_virtual_server](https://github.com/ansible-role-fad-slb-virtual-server)

This (these) role(s) is opiniated for my personal needs, which is to make the configuration setups is as simple as possible for L7 HTTP content routings. Most of the roles/configs only needs one or two required parameters, and for others takes my personal needs as default value (or reuse the previously mentioned required parameter).

Still, those are still kinda optional. Since I'm just setting them as a "default" value, you can compare the "minimal" and "complete" example in [test folder](tests/), and then overwrite them with your own value by following the "complete" example.

This role also compile the variable to be app-based instead of object-based.

[!Note]
This `fad_server_load_balnce` role actually only contains tasks that delete the entries that have `state: absent` in them. For the creation itself is actually handled individually by their own role. I did this because of the create and delete dependency is the reverse of each other.

## Usage

### Install Role

```
ansible-galaxy install ndkprd.fad_server_load_balance
```

### Hosts Example

```
[fortiadc]
fad-01 ansible_host=fad-01.infra.ndkprd.com ansible_connection=local fad_apitoken=mysupersecrettoken fad_vdom=root
```

### Playbook Example

See [test folder](tests/).

### About Tags

Each task is tagged with their role name, which you can skip if you want:
- fad_slb_real_server
- fad_slb_real_server_pool
- fad_slb_content_routing
- fad_slb_virtual_server

There's also a some kind of pre-task and post-task that run before and after create/update tasks to compare the value of before and after create/update tasks, tagged with the above tag and an additional `debug` tag.

## Limitation

Only developed and tested against FortiADC 7.0.

## License

MIT, use at your own risk.
