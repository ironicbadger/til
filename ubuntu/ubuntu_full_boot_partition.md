### Fix a full /boot partition on Ubuntu

If `apt` won't work properly because `/boot` is full you only have one option to clean up old kernels which are installed but not used. This one liner will list

```
    apt-get remove `dpkg --list 'linux-image*' |grep ^ii | awk '{print $2}'\ | grep -v \`uname -r\``
```

Then run `apt-get update` then `autoremove` and so on.

- Source(s)
  - [askubuntu](http://askubuntu.com/questions/345588/what-is-the-safest-way-to-clean-up-boot-partition)
