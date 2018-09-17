# ansible-owncloud

Installs a owncloud server as docker container.
This role is only tested on ubuntu 18.04.

## System requirements

* Docker
* docker-compose
* Systemd

## Role requirements

* python-docker package

## Tasks

* Build docker image locally
* Create volume paths for docker container
* Create docker-compose file
* Setup systemd unit file
* Start/Restart service

## Role parameters

| Variable      | Type | Mandatory? | Default | Description           |
|---------------|------|------------|---------|-----------------------|
| version       | text | no         | 10.0.3  | Owncloud version    |
| volumes.data  | text   | no       | <empty>  | Local path to owncloud data volume |
| volumes.config | text | no | <empty> | Local path to owncloud config volume       |
| volumes.database | text | no | <empty> | Local path to database data volume       |
| publish.port     | text | no | <empty> | Port to be published                     |
| publish.interface | text | no | 0.0.0.0 | Interface to be published               |
| database.user     | text | no | <empty> | Database connection user name           |
| database.password | text | no | <empty> | Database connection password            |

## Usage

### requirements.yml

```
- name: install-owncloud
  src: https://github.com/flandiGT/ansible-owncloud.git
  scm: git
```

### Example Playbook

Usage (without parameters):

    - hosts: servers
      roles:
         - { role: install-owncloud }

Usage (with parameters):

    - hosts: servers
      roles:
      - role: install-owncloud
        version: 10.0.3
        volumes:
          data: /srv/docker/owncloud/data
          config: /srv/docker/owncloud/config
          database: /srv/docker/owncloud/database
        publish:
          port: 8090
          interface: 0.0.0.0
        database:
          user: postgres
          password: my_super_secret_password
