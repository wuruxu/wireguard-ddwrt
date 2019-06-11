# setup wireguard @ ddwrt

* install latest ddwrt firmware, [BS build](https://download1.dd-wrt.com/dd-wrtv2/downloads/betas/2019/05-27-2019-r39866/) is recommended
* setup endpoint(VPN SERVER) config following [WireGuard](https://www.wireguard.com/)
* setup peer config in ddwrt ![SETUP/TUNNEL](images/eop-tunnel.asp.png)
* add startup firewall rules for wireguard oet1 (Administration/Command)
```bash
ip rule add from 192.168.18.0/24 lookup 100
ip route add table 100 default via 192.168.2.1 dev oet1
iptables -t nat -A POSTROUTING -s 192.168.18.0/24 -o oet1 -j MASQUERADE
```

* add a new VAP in Wireless_Basic.asp ![VAP](images/vap.png)

* Services -> Services and ensure that DNSMasq is enabled, Enter the following into Additional DNSMasq Options: **dhcp-option=wl1.1,6,8.8.8.8,1.1.1.1** ![DNSMASQ](images/dnsmasq.png)

Now after you connect to VAP, all traffic will forward to wireguard

NOTICE: MUST `disable AP Isolation` for Google home 
