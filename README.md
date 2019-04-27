# ansible-role-telegraf

[![Build Status](https://travis-ci.org/BadFever/ansible-role-telegraf.svg?branch=master)](https://travis-ci.org/BadFever/ansible-role-telegraf)

Installs telegraf on CentOS 7 for client monitoring only.

## Requirements

None.

## Role Variables

Available variables are listed below, along with default values (see defaults/main.yml):

The InfluxData repository url.

```yaml
influxdata_yum_repo_url: https://repos.influxdata.com/rhel/{{ ansible_distribution_major_version }}/{{ ansible_architecture }}/stable
```

The InfluxData gpg key url.

```yaml
influxdata_gpg_url: https://repos.influxdata.com/influxdb.key
```

The url of an influxdb instance including port.

```yaml
influxdb_url: http://localhost:8086
```

The name of the influxdb database.

```yaml
influxdb_database: telegraf_
```

The user for accessing the infuxdb via http.

```yaml
influxdb_user: telegraf
```

The users password.

```yaml
influxdb_password: telegraf
```

The telegraf batch size.

```yaml
telegraf_metric_batch_size: 1000
```

The telegraf buffer size

```yaml
telegraf_metric_buffer_limit: 10000
```

## Dependencies

None.

## Example Playbook

```yaml
- hosts: all
  remote_user: root
  vars:
    influxdb_url: http://localhost:8086
    influxdb_database: telegraf
    influxdb_user: telegraf
    influxdb_password: telegraf
  roles:
    - ansible-role-telegraf
```

## License

MIT


[[outputs.influxdb]]

  urls = ["{{ influxdb_url }}"]
  database = "{{ influxdb_database }}"
  # database_tag = ""
  skip_database_creation = true

  ## Name of existing retention policy to write to.  Empty string writes to
  ## the default retention policy.  Only takes effect when using HTTP.
  # retention_policy = ""

  # timeout = "5s"
  ## HTTP Basic Auth
  username = "{{ influxdb_user }}"
  password = "{{ influxdb_password }}"

  ## Optional TLS Config for use on HTTP connections.
  # tls_ca = "/etc/telegraf/ca.pem"
  # tls_cert = "/etc/telegraf/cert.pem"
  # tls_key = "/etc/telegraf/key.pem"
  ## Use TLS but skip chain & host verification
  # insecure_skip_verify = false


telegraf_vsphere_vcenters: "\"https://vcsa/sdk\""
telegraf_vsphere_username: "telegraf@vsphere.local"
telegraf_vsphere_password: "telegraf"
telegraf_vsphere_interval: "60s"
telegraf_vsphere_max_query_objects: 256
telegraf_vsphere_max_query_metrics: 256
telegraf_vsphere_collect_concurrency: 1
telegraf_vsphere_discover_concurrency: 1
telegraf_vsphere_object_discovery_interval: "300s"
telegraf_vsphere_timeout: "60s"
telegraf_vsphere_insecure_skip_verify: "true"

