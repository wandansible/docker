Ansible role: Docker
====================

Install docker and configure the docker daemon. Optionally, install docker-compose.

Role Variables
--------------

```
ENTRY POINT: main - Install and configure docker

        Install docker and configure the docker daemon. Optionally,
        install docker-compose.

OPTIONS (= is mandatory):

- docker_apt_key_fingerprint
        Fingerprint for docker apt signing key
        [Default: (null)]
        type: str

- docker_compose_install
        Whether or not to install docker compose
        [Default: False]
        type: bool

- docker_daemon
        Configuration for the docker daemon.
        See https://docs.docker.com/engine/reference/commandline/dockerd/#daemon-configuration-file for configuration options
        [Default: (null)]
        type: dict
```

Installation
------------

This role can either be installed manually with the ansible-galaxy CLI tool:

    ansible-galaxy install git+https://github.com/wandansible/docker,main,wandansible.docker
     
Or, by adding the following to `requirements.yml`:

    - name: wandansible.docker
      src: https://github.com/wandansible/docker

Roles listed in `requirements.yml` can be installed with the following ansible-galaxy command:

    ansible-galaxy install -r requirements.yml

Example Playbook
----------------

    - hosts: docker_hosts
      roles:
         - role: wandansible.docker
           become: true
           vars:
             docker_compose_install: true
             docker_daemon:
               hosts:
                 - unix:///var/run/docker.sock
               live-restore: true
               iptables: false
               ip-forward: false
               ip-masq: false
