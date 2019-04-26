# ansible-role-telegraf

[![Build Status](https://travis-ci.org/BadFever/ansible-role-telegraf.svg?branch=master)](https://travis-ci.org/BadFever/ansible-role-telegraf)

Installs telegraf on CentOS 7 for client monitoring.

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
influxdb_database: telegraf
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

The vSphere plugin vCenters.

```yaml
telegraf_vsphere_vcenters: ["https://vcsa/sdk"]
```

Enable or disable the vSphere input plugin.

```yaml
telegraf_vsphere_plugin_enabled: false
```

The vSphere plugin vCenter user.

```yaml
telegraf_vsphere_username: "telegraf@vsphere.local"
```

The vSphere plugin vCenter password

```yaml
telegraf_vsphere_password: "telegraf"
```

The vSphere plugin collector interval.

```yaml
telegraf_vsphere_interval: "60s"
```

The vSphere plugin object query limit.

```yaml
telegraf_vsphere_max_query_objects: 256
```

The vSphere plugin object metric limit.

```yaml
telegraf_vsphere_max_query_metrics: 256
```

The vSphere plugin object collectors go routines.

```yaml
telegraf_vsphere_collect_concurrency: 1
```

The vSphere plugin object discover go routines.

```yaml
telegraf_vsphere_discover_concurrency: 1
```

The vSphere plugin object discovery interval.

```yaml
telegraf_vsphere_object_discovery_interval: "300s"
```

The vSphere plugin api request timeout.

```yaml
telegraf_vsphere_timeout: "60s"
```

Skip insecure vCenter certificates.

```yaml
telegraf_vsphere_insecure_skip_verify: true
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
