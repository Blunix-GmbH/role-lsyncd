## SSH
- create ssh keypair on this machine for lsyncd_master_user
- put the public key into authorized_keys for lsyncd_client_user

## fs inotify max user watches
- scan dir to sync: /proc/sys/fs/inotify/max_user_watches
  and increase automatically? (see readme for manual process)
