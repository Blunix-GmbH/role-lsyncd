Ansible Role lsyncd
====================

This role configures a continously running rsync daemon called [lsyncd](https://axkibe.github.io/lsyncd/).


Example Play
------------

```yaml
- hosts: foo
  vars:
    TODO

  roles:
    - blunix.role-lsyncd
```


## Requirements

**Passwordless SSH**  
This role requires the user running `lsyncd` to have passwordless SSH access configured to the client machine.
A SSH keypair has to be set up on the `lsyncd` machine and its public key installed on the "client" machine.

**Sysctl settings**  
As `lsyncd` `inotifywatch`'es the `source` directory for changes. `/proc/sys/fs/inotify/max_user_watches` may have to be increased accordingly. Increasing this setting may be required to prevent the message:
```
lsyncd: Error, Terminating since out of inotify watches.#012Consider increasing /proc/sys/fs/inotify/max_user_watches
```

You should set a number higher than the amount of subdirectories in the directory that is to be kept in sync, for example:
```
root@web-one.example.com ~ # find /var/www -type d | wc -l | tail -n 1
25410
root@web-two.example.com /var $ cat /proc/sys/fs/inotify/max_user_watches
8192
root@web-two.example.com /var $ echo '8192 * 8' | bc
65536
root@web-two.example.com /var $ echo 65536 > /proc/sys/fs/inotify/max_user_watches
```

in `/var/log/syslog`. The `lsyncd` status logfile `/var/log/lsyncd-status.log` will also give you this information:
```
root@web-one.example.com ~ # cat /var/log/lsyncd-status.log | grep Inotify
Inotify watching 25410 directories
```


License
=======

Apache

Author Information
==================

Service and support for orchestrated hosting environments, continuous integration/deployment/delivery and various Linux and open-source technology stacks are available from:

```
Blunix GmbH - Professional Linux Service
Glogauer Straße 21
10999 Berlin - Germany

Web: www.blunix.org
Email: mailto:service@blunix.org
```
