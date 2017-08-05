### Setup DDns on a Synology NAS

This is simplest way I found to update dynamic DNS with Namecheap on a Synology NAS. I performed this on a Synology DS215j.

First, install PERL from the official package lists in the Synology Package Center. Next, using the two .spk files in this repository, install the `Init_3rdparty_1.9-003.spk` using the "manual install" option. Finally install the ddns client spk itself again using the "manual install option".

Next, you need to configure a dynamic hostname to be updated in Namecheap and grab the DDNS password and configure it in the example file below...

So far as I can tell, this file should live in `/tmp/cache/ddclient/ddclient.conf` but there's also a second copy appeared in `/volume1/@appstore/ddnsupdater/ddclient.conf`, not sure which to use.

```
######################################################################
##
## ddclient.conf created 06/01/2014 17:14
##
######################################################################
daemon=300
max-interval=22d
ssl=no
syslog=yes
pid=/var/run/ddclient.pid
file=/tmp/cache/ddclient/ddclient.conf
cache=/tmp/cache/ddclient/ddclient.cache
notify-failure=@administrators

# DDNS Provider Parameters Section
use=web, web=dynamicdns.park-your-domain.com/getip
protocol=namecheap
server=dynamicdns.park-your-domain.com
login=tld.domainhere
password=ddnspass
subdomainhere
```
