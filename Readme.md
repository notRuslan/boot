Login to system without password:

1.  init=/bin/sh
```
find linux16 or linuxefi
add at the end of line init=/bin/sh
After boot:
 mount -o remount,rw /
Check:
    mount | grep ^/
    echo NEW_PASS | passwd --stdin root
  Fix SElinux issues (for Vagrant it's better than /.autorelabel):
    /usr/sbin/load_policy -i
    /usr/sbin/restorecon -Rv /etc
   exit;
   sync;
   echo 1 > /proc/sys/kernel/sysrq;
   echo b /proc/sysrq-trigger;
```
2. Method  rd.break
```
find linux16 or linuxefi
add at the end of line rd.break
After boot:
  mount -o remount,rw /sysroot
  chroot /sysroot
  passwd root
  touch /.autorelabel (but better load_policy -i)
  exit;
  systemctl reboot
```
3. Method  rw init=/sysroot/bin/sh
```
find linux16 or linuxefi
find ro and change to rw init=/sysroot/bin/sh
After boot:
    echo NEW_PASS | passwd --stdin root
     Fix SElinux issues (for Vagrant it's better than /.autorelabel):
       /usr/sbin/load_policy -i
       /usr/sbin/restorecon -Rv /etc
      exit;
      sync;
      echo 1 > /proc/sys/kernel/sysrq;
      echo b /proc/sysrq-trigger; 

```