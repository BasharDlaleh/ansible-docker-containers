Role Name
=========

docker_containers

An Ansible Role to manage docker containers on Linux servers. 

Supported docker operations : 

- run containers
- stop containers
- start containers
- restart containers
- show containers states

Requirements
------------

The below requirements are needed on every host that this role executes on

Docker API >= 1.20
Docker SDK for Python
Docker SDK for Python >= 1.8.0 (use docker-py for Python 2.6)

example on Ubuntu

- sudo apt install -y python3
- sudo apt install -y python3-pip
- sudo pip3 install docker

Note: for operating systems that do not support Python 3, the module 'docker-py' should be installed instead of 'docker'

Role Variables
--------------

This role uses group vars to define what containers we want to manage, so you need to create group_vars folder in your work directory and define your groups inside it, please see the notes in docker-servers.yml example group vars file for more details
 
Dependencies
------------

None.

Example Playbook
----------------

    - hosts: docker-servers
      vars:
        ansible_python_interpreter: /usr/bin/python3
      roles:
         - { role: bashardlaleh.docker_containers }

*Inside `group_vars/docker-servers.yml`*:

	containers:
	- name: nodeapp1
	  image: nodeapp
	  ports:
	   - "1111:8081"
	  container_ports:
	   - 8081
	  mounts: 
           - source: /tmp
           - target: /tmp
           - type: bind
	  env:
	    APPID: '1111'

	- name: nodeapp2
	  image: nodeapp
	  ports:
	   - "2222:8081"
	  container_ports:
	   - 8081
	  mounts: false
	  env: false

License
-------

MIT / BSD
