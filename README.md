Role Name
=========

bashardlaleh.docker.containers

An Ansible Role that manages docker containers on Linux servers. 

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

This role uses group vars to define what containers we want to manage, please see the notes in docker-servers.yml file for more details
 
Dependencies
------------

None.

Example Playbook
----------------

    - hosts: docker-servers
      roles:
         - { role: bashardlaleh.docker.containers }

*Inside `group_vars/docker-servers.yml`*:

	containers:
	- name: nodeapp2
	  image: nodeapp
	  ports:
	   - "2222:8081"
	  container_ports:
	   - 8081
	  volumes: 
           - /tmp:/tmp
	  env:
	    APPID: '2222'

	- name: nodeapp3
	  image: nodeapp
	  ports:
	   - "3333:8081"
	  container_ports:
	   - 8081
	  volumes: false
	  env: false

License
-------

MIT / BSD
