Role Name
=========

An [Ansible] role to provision a [Docker] swarm cluster.

Requirements
------------

Install [Ansible] roles required:
```
sudo ansible-galaxy install -r requirements.yml
```

Role Variables
--------------

```
---
---
# defaults file for ansible-docker-swarm

# Define Docker interface to auto fill `docker_swarm_addr`
docker_swarm_interface: "enp0s8"

# Define Docker swarm listen and advertise address
docker_swarm_addr: "{{ hostvars[inventory_hostname]['ansible_' + docker_swarm_interface]['ipv4']['address'] }}"

# Define Docker swarm listen port
docker_swarm_port: "2377"

# Define Docker swarm data path port
docker_swarm_data_path_port: ''


# Define Ansible group which contains your Docker swarm managers
docker_swarm_managers_ansible_group: 'docker-swarm-managers'

# Define Ansible group which contains you Docker swarm workers
docker_swarm_workers_ansible_group: 'docker-swarm-workers'

# Defines first node in docker_swarm_managers_ansible_group as primary
docker_swarm_primary_manager: '{{ groups[docker_swarm_managers_ansible_group][0] }}'


# Define Docker swarm network customizations
docker_swarm_config_networks: false

# Network: see community.docker.docker_network
docker_swarm_networks: []
  # - name: 'my_net'
  #   driver: 'overlay'
  #   state: 'present'
  # - name: 'test'
  #   driver: 'overlay'
  #   state: 'absent'


# Define Docker swarm setting customizations
docker_swarm_config_settings: false

# Setting: Validity period for node certificates (default 2160h0m0s)
docker_swarm_cert_expiry: '2160h0m0s'

# Setting: Dispatcher heartbeat period (default 5s)
docker_swarm_dispatcher_heartbeat_duration: '5s'

# Setting: Task history retention limit (default 5)
docker_swarm_task_history_limit: '5'
```

Dependencies
------------

None

Example Playbook
----------------

```
- hosts: docker_hosts
  become: true
  vars:
  roles:
    - role: ansible-docker
    - role: ansible-docker-swarm
  tasks:
```

License
-------

BSD

Author Information
------------------


Larry Smith Jr.
- @mrlesmithjr
- http://everythingshouldbevirtual.com
- mrlesmithjr [at] gmail.com

[Ansible]: <https://www.ansible.com>
[Docker]: <https://www.docker.com>
