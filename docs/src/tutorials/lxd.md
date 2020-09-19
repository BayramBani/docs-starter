# LXD
---

* SSH 

```bash
iptables -t nat -A PREROUTING -i eth0 -p tcp --dport 2222 -j DNAT --to 10.187.138.67:22
```

* LAN Network

```bash
lxc profile device set default eth0 parent eth0
lxc profile device set default eth0 nictype macvlan
```

* NAT Network 

```bash
lxc profile device set default eth0 parent lxdbr0
lxc profile device set default eth0 nictype bridged
```

* OpenStack

```bash
nova boot --image=trusty --flavor=m1.tiny --nic net-id=55fd2431-af25-4d77-b67c-9f88263a3547 --security-group=default --key-name=cloud  lxdOpen
```



