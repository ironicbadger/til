### QEMU guest has no internet

If the behavior you are seeing is host can access the guest, and guest can access the host, but the guest can't access other machines on the network or visa versa... probably the host's firewall is blocking access.

See: https://bugs.launchpad.net/ubuntu/+source/ufw/+bug/573461

Specifically, this section: "The final step is to disable netfilter on the bridge:

```bash
# cat >> /etc/sysctl.conf <<EOF
net.bridge.bridge-nf-call-ip6tables = 0
net.bridge.bridge-nf-call-iptables = 0
net.bridge.bridge-nf-call-arptables = 0
EOF
```

- Source(s)
  - [1](https://askubuntu.com/a/307600)
