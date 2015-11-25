## just a fork
I'm just experimenting trying to set up a metrics server.

# Changelog
- Fixed InfluxDB download link
- Fixed Grafana download link
  - Fixed Grafana install (it's a .deb now instead of a .tar.gz)

# InfluxDB 0.9.5 + Grafana 2.5 sandbox

Runs a VM with influxdb and grafana. You can use dashboard.yml and roles to install in a production server, just tune influxdb address.

# Requirements

- Vagrant

# Usage
## Locally with Vagrant

```
$ vagrant up
$ open http://192.168.33.21:3000 # on your browser for Grafana
```

Log into Grafana with the defaults (user 'admin', password 'admin').

## Remotely with your cloud of preference

    - Add your hostname to ansible hosts file (/etc/ansible/hosts or any other location, you can change that)
        [dashboard]
        host1 ansible_ssh_host=192.168.1.1

    - Make sure you can ssh into it using keys
        ssh root@192.168.1.1

    - Run
        ansible-playbook -l host dashboard.yml

    - Send me a pull request in case it doesn't works.
