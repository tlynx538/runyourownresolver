# runyourownresolver
Run your own recursive DNS resolver


## Update Packages and Repositories
`sudo apt-get update`
## Installing Unbound
`sudo apt-get install unbound`
## Configuring Unbound
`sudo mv  /etc/unbound /etc/unbound.dist`

`mkdir /etc/unbound`

`chown unbound.unbound /etc/unbound`

## Copy the following unbound configuration
```
server:
    interface: 127.0.0.1
    interface: ::0
    access-control: 192.168.0.0/16 allow
    verbosity: 1

#access-control: 10.0.0.0/16 allow
access-control: 127.0.0.1/32 allow

root-hints: "/etc/unbound/root.hints"
use-syslog: yes
log-time-ascii: yes

# logfile: /var/log/unbound

log-queries: yes
```
## Intializing Unbound
`sudo -u unbound unbound-control-setup`

`sudo curl --output /etc/unbound/root.hints https://www.internic.net/domain/named.cache`

## Checking the unbound configuration
`sudo unbound-checkconf`

## Start Unbound
`sudo /etc/init.d/unbound start`