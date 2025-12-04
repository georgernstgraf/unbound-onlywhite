# Installation virtual

## tunables

/etc/NetworkManager/conf.d/99-usb-passthrough.conf

- hw.usb.quirk.0
- 0x2357 0x0601 0 0xffff UQ_CFG_INDEX_1
- carrier loss on ure

## usb eth festschreiben

`chmod +x /usr/local/sbin/usb_nic_rename.sh`

## System DNS: System -> Settings -> General

- DNS Servers: Leer lassen oder machen
- check: Allow DNS server list to be overridden by DHCP/PPP on WAN
- check: Do not use the local DNS service as a nameserver for this system

### Unbound forward only: Services -> Unbound DNS -> Query Forwarding

- check: Use System Nameservers

### Unbound log queryies: Services -> Unbound DNS -> Advanced

- check: log Queries
- check: log Replies
- check: tag Queries and Replies

### Bundle alls DNS Traffic to unbound: Firewall -> NAT -> Port Forward

- redirect all DNS Traffic that targets "not this firewall" to 127.0.0.1

### DOH add Alias: Firewall -> Aliases -> Add

- Content Box: <https://raw.githubusercontent.com/crypt0rr/public-doh-servers/main/ipv4.list>

### DOH drop 443: Firewall -> Rules -> LAN

- block incoming https traffic to the DOH alias

## NMAP CRON

- create /usr/local/opnsense/scripts/custom/nmap_cron.sh
- create /usr/local/opnsense/service/conf/actions.d/actions_nmap.conf
- run `service configd restart`
- create the cronjob with the gui

## ALIASES for .profile

- `alias ub='unbound-control -c /var/unbound/unbound.conf`
- `alias ut='tail -F /var/log/resolver/latest.log'`
