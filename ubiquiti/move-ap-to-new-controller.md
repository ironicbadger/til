### Transfer adoption of a Ubiquiti AP

Ubiquiti APs are 'adopted' by the control software, here's how to migrate an already configured AP to a new controller.

    nmap 192.168.1.0/24 -p 22 -oG - |grep open
    ssh adminuser@AP-IP
    syswrapper.sh restore-default
    === reboot (wait 20 secs) ===
    ssh ubnt@AP-IP
    password = ubnt (default)
    mca-cli
    set-inform http://controllerip:8080/inform

    === adopt AP on the controller ===
    === when state = disconnected after adoption continue here ===

    set-inform http://controllerip:8080/inform
    exit

Yes, you really do run the same `set-inform` command twice either side of 'adopting' the AP on the controller. Seems dumb to me.

- Source(s)
  - [1](http://helpdesk.maytechgroup.com/support/solutions/articles/3000008280-how-to-move-a-ubiquiti-unifi-access-point-to-a-new-controller-v2-x-)
