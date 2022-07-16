[https://wiki.debian.org/Network?action=show&redirect=CategoryNetwork](https://wiki.debian.org/Network?action=show&redirect=CategoryNetwork)

[https://www.youtube.com/channel/UCqxgclFS32S3ayVweoCFQCg/videos](https://www.youtube.com/channel/UCqxgclFS32S3ayVweoCFQCg/videos)

```jsx
ip link
```

```jsx
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: eno1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast master vmbr0 state UP mode DEFAULT group default qlen 1000
    link/ether 48:0f:cf:4f:7c:c7 brd ff:ff:ff:ff:ff:ff
    altname enp0s25
7: vmbr0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP mode DEFAULT group default qlen 1000
    link/ether 48:0f:cf:4f:7c:c7 brd ff:ff:ff:ff:ff:ff
8: vmbr1: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN mode DEFAULT group default qlen 1000
    link/ether ee:ef:e9:1d:e4:63 brd ff:ff:ff:ff:ff:ff
21: tap100i0: <BROADCAST,MULTICAST,PROMISC,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast master fwbr100i0 state UNKNOWN mode DEFAULT group default qlen 1000
    link/ether 42:0e:e6:d2:34:83 brd ff:ff:ff:ff:ff:ff
22: fwbr100i0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP mode DEFAULT group default qlen 1000
    link/ether e2:07:2e:f7:be:99 brd ff:ff:ff:ff:ff:ff
23: fwpr100p0@fwln100i0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue master vmbr0 state UP mode DEFAULT group default qlen 1000
    link/ether 6e:9d:32:ad:e4:57 brd ff:ff:ff:ff:ff:ff
24: fwln100i0@fwpr100p0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue master fwbr100i0 state UP mode DEFAULT group default qlen 1000
    link/ether f6:aa:c6:9e:d9:91 brd ff:ff:ff:ff:ff:ff
```

```jsx
ip a
```

```jsx
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: eno1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast master vmbr0 state UP group default qlen 1000
    link/ether 48:0f:cf:4f:7c:c7 brd ff:ff:ff:ff:ff:ff
    altname enp0s25
7: vmbr0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default qlen 1000
    link/ether 48:0f:cf:4f:7c:c7 brd ff:ff:ff:ff:ff:ff
    inet 172.16.100.164/24 scope global vmbr0
       valid_lft forever preferred_lft forever
    inet6 fe80::4a0f:cfff:fe4f:7cc7/64 scope link
       valid_lft forever preferred_lft forever
8: vmbr1: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN group default qlen 1000
    link/ether ee:ef:e9:1d:e4:63 brd ff:ff:ff:ff:ff:ff
    inet 192.168.40.0/24 scope global vmbr1
       valid_lft forever preferred_lft forever
    inet6 fe80::ecef:e9ff:fe1d:e463/64 scope link
       valid_lft forever preferred_lft forever
21: tap100i0: <BROADCAST,MULTICAST,PROMISC,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast master fwbr100i0 state UNKNOWN group default qlen 1000
    link/ether 42:0e:e6:d2:34:83 brd ff:ff:ff:ff:ff:ff
22: fwbr100i0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default qlen 1000
    link/ether e2:07:2e:f7:be:99 brd ff:ff:ff:ff:ff:ff
23: fwpr100p0@fwln100i0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue master vmbr0 state UP group default qlen 1000
    link/ether 6e:9d:32:ad:e4:57 brd ff:ff:ff:ff:ff:ff
24: fwln100i0@fwpr100p0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue master fwbr100i0 state UP group default qlen 1000
    link/ether f6:aa:c6:9e:d9:91 brd ff:ff:ff:ff:ff:ff
```

nano /etc/network/interfaces

```jsx
auto lo
iface lo inet loopback

auto eno1
iface eno1 inet manual

auto enp0s8 // autostart interface
iface enp0s8 inet static
        address 172.16.100.168
        netmask 255.255.255.0
        dns-nameserver 8.8.8.8  // if you installed "[resolvconf](https://wiki.debian.org/resolv.conf)" package you didn't need use of this option
        dns-nameserver 1.1.1.1
```

```jsx
ifup enp0s8 
ifdown enp0s8 
```