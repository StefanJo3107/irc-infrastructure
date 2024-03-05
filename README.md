# IRC Infrastrucure for badusb devices
IRC infrastrucure consisting of Ergo IRC server, two MySQL DBs for master/slave replication and Apache server for serving static files (payloads).

## How to run
You will need to have Vagrant with either VirtualBox or KVM/qemu, python3 and Ansible installed in order to build and provision the infrastrucure.<br/>
Once you have those installed, you can run ```vagrant up``` command to start up the VMs. In order to provision the machines, run ```vagrant provision```.

## Project configuration
There are number of parameters you can configure for Ergo server. Most of them you can find in the `roles/ergo/defaults/main.yml` and `playbooks/irc-server/vars.yml` files:
```---
# defaults file for ergo
ergo_install_dir: "/usr/local/src/ergo"
ergo_github_releases_api: "https://api.github.com/repos/ergochat/ergo/releases/latest"
ergo_install_arch: "'linux-x86_64'"

ergo_text_port: 6667
ergo_tls_port: 6697

ergo_log_level: "info"
ergo_registration_enabled: true
ergo_max_concurrent_conns: 32
ergo_suppress_lusers: false

ergo_history_enabled: false
ergo_history_autoresize_window: 7d
ergo_history_autoreplay_on_join: 100

ergo_email_verification_enabled: false
ergo_email_verification_blacklist_regexes: []

ergo_mysql_enabled: false

#server
ergo_server_password: "$2a$04$6l6lZijBYJta.N1O/dB1ve3lnTpjRHP4zijqXTw4Vf8rEEvaeSpMi"
#admin
ergo_admin_password: "$2a$04$w9.CPmz/qltTZOsYWvhl2.5.yQxVZpZU1p0DEDkzMx0zOOEJBFAsy"
```

```---
firewall_allowed_tcp_ports:
    - "22"
    - "6667"
    - "6697"

ergo_network_name: "BadusbNetwork"
ergo_server_name: "badusb.test.org"
ergo_motd_path: "ergo.motd"

ergo_history_persistent: false
ergo_mysql_enabled: false
ergo_mysql_host: "192.168.60.5"
ergo_mysql_port: 3306
ergo_mysql_user: "badusb_irc"
ergo_mysql_password: "password"
ergo_mysql_dbname: "badusb_irc_db"
```
