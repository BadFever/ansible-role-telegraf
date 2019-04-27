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
  roles:
    - ansible-role-telegraf
```

## License

MIT


