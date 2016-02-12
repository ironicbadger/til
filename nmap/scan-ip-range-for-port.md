### Scan IP range for a specific port with `nmap`

Perform a scan with nmap on a specific IP range for machines listening on port 22 (SSH).

`nmap 192.168.1.0/24 -p 22 -oG - | grep open`

Other example(s):

`nmap -sV --open 192.168.1.0/24  -p22 | grep interesting -i`

- Source(s)
  - [1](http://helpdesk.maytechgroup.com/support/solutions/articles/3000008280-how-to-move-a-ubiquiti-unifi-access-point-to-a-new-controller-v2-x-)
  - [2](http://johanharjono.com/scan-lan-for-ssh-able-hosts.html)
