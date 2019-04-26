# ansible-role-tick

Installs telegraf on CentOS 7 for client monitoring.

## Requirements

None.

## Role Variables

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

## Manual Installation

```bash
# ntp
yum -y install ntp
systemctl start ntpd
systemctl enable ntpd

cat <<EOF | sudo tee /etc/yum.repos.d/influxdata.repo
[influxdb]
name = InfluxData Repository - RHEL \$releasever
baseurl = https://repos.influxdata.com/rhel/\$releasever/\$basearch/stable
enabled = 1
gpgcheck = 1
gpgkey = https://repos.influxdata.com/influxdb.key
EOF

# install telegraf
yum -y install telegraf

# generate config
# telegraf --input-filter cpu:disk:diskio:dns_query:mem:net:netstat:ping:system: --output-filter influxdb config > telegraf.conf


# start and enable service
systemctl start telegraf
systemctl enable telegraf
```

### Database User

```bash
influx
CREATE USER admin WITH PASSWORD 'fever.123WL' WITH ALL PRIVILEGES
CREATE USER telegraf WITH PASSWORD 'telegraf'
GRANT WRITE ON telegraf TO telegraf

REVOKE ALL PRIVILEGES FROM telegraf
influx -username telegraf -password telegraf
```