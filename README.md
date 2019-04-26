# ansible-role-tick

Setup TICK Stack (Telegraf, InfluxDB, Chronograf, Kapacitor) and Grafana.

## Requirements

None

## Role Variables

## Dependencies

## Example Playbook

```yaml
- hosts: all
  remote_user: root
  roles:
    - ansible-role-nginx
    - ansible-role-tick
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
telegraf --input-filter cpu:disk:diskio:dns_query:mem:net:netstat:ping:system: --output-filter influxdb config > telegraf.conf

# syslog reciever
firewall-cmd --zone=internal --add-port=6514/tcp --permanent
firewall-cmd --reload

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