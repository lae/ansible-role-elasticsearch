[![Build Status](https://travis-ci.org/fireeye-ops/ansible-role-elasticsearch.svg?branch=master)](https://travis-ci.org/fireeye-ops/ansible-role-elasticsearch)
[![Galaxy Role](https://img.shields.io/badge/ansible--galaxy-elasticsearch-blue.svg)](https://galaxy.ansible.com/fireeye-ops/elasticsearch/)

elasticsearch
=========

Installs and configures Elasticsearch as part of a multi-node cluster.

## Notes

This Ansible role does not start or restart Elasticsearch on changes as there 
is a lack of configuration file validation tools. This role will inform you if 
a restart is needed, however, so please do so then.

Please note that most configuration decisions (like the above) within this role 
are meant for production clusters, which may not make this role suitable for 
dev environments. (The intention is to cater to both eventually.)

## Role Variables

### Mandatory Variables

You must define `elasticsearch_cluster_name` to identify your Elasticsearch 
cluster, either in the playbook or in a group variables file.

### Optional Variables

The following variables are used in the elasticsearch configuration file. 
Please review `templates/elasticsearch.yml.j2` for more detailed notes.
Most variables below have saner defaults in this file.

Likely to be defined per host:

```
elasticsearch_node_name: machine03
elasticsearch_node_attributes: []
elasticsearch_path_data: /mnt/disk1,/mnt/disk2,/mnt/disk3
```

Likely to be defined per cluster/group (or `all`):

```
elasticsearch_major_minor_version: 2.3
elasticsearch_path_logs: /var/log/elasticsearch
elasticsearch_http_port: 9210
elasticsearch_network_host: "{{ ansible_default_ipv4.address }}"
elasticsearch_disable_deletion_of_all_indices: false
```

Dependencies
------------

* williamyeh.oracle-java

Example Playbook
----------------

```
---
- hosts: cluster01
  become: True
  roles:
    - fireeye-ops.elasticsearch
  vars:
    elasticsearch_cluster_name: cluster01
    elasticsearch_hostgroup: cluster01
    elasticsearch_hostgroup_discovery: cluster01_discovery
    elasticsearch_network_host: _global_
```

License
-------

MIT

Author Information
------------------

TBD
