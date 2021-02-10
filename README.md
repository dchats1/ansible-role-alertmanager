Alertmanager
=========

Deploy Alertmanager in podman containers in as a single instance or HA pair. https://prometheus.io/docs/alerting/latest/alertmanager/

Requirements
------------

This requires the containers.podman collection: https://galaxy.ansible.com/containers/podman Recommended 1.4.1 or later

Role Variables
--------------

Variable                           | Description
-----------------------------------|-------------------
alertmanager_version               | Version of Alertmanager. (Default: 0.21.0)
alertmanager_base_dir              | Directory to store alert manager configs. (Defaults: /var/lib/containers)
alertmanager_podman_network        | Podman network to deploy containers. (Default: podman)
alertmanager_hostname              | Short hostname for pods. (Default: alertmanager)
alertmanager_domain                | Domain name for pods. (Default: example.com)
alertmanager_web_listen_port       | Port for --web.listen-address (Default: 9093)
alertmanager_cluster_listen_port   | Port for --cluster.listen-address (Default: 9094)
alertmanager_ha_replicas           | Number of alertmanager replicas. (Default: 1)
alertmanager_flags                 | Flags to pass to alert manager. (Default: [ '--web.listen-address=0.0.0.0:{{ alertmanager_web_listen_port }}', '--config.file=/etc/alertmanager/alertmanager.yml', '--storage.path=/alertmanager'] )
alertmanager_global_config         | Global config. See example in comments and down below.
alertmanager_route_config          | Route config. See example in comments and down below.
alertmanager_receivers_config      | Receivers config. See example in comments and down below.

```
alertmanager_global_config: []
#alertmanager_global_config: |
#  smtp_smarthost: 'localhost:25'
#  smtp_from: 'alertmanager@example.com'
```

```
alertmanager_route_config: []
#alertmanager_route_config: |
#  receiver: 'example-email'
#  group_by: [prometheus_cluster]
#  group_wait: 30s
#  group_interval: 5m
#  repeat_interal: 3h
#  routes:
#  - match:
#      severity: critial
#    receiver: example-email
```

```
alertmanager_receivers_config: []
#alertmanager_receivers_config: |
#  - name: 'example-email'
#    email_configs:
#    - to: 'my-team-alerts@example.com'
```

Dependencies
------------

No dependencies at this time

Example Playbook
----------------

```
- hosts: podman_host
  roles:
    - alertmanager

License
-------

BSD

Author Information
------------------

David Chatterton
david@davidchatterton.com
