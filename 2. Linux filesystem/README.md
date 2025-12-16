# Linux filesystem

partition
: Physically continuous section of a disk.  On modern systems it just appears like a continuous section

filesystem
: method of storing or finding files on HDD

FHS
: Filesystem Hierarchy Standard


| Directory | Purpose |
| :-------- | ------- |
| /bin/         | essential user commands |
|               | essential commands to boot the system |
| /boot/        | static files of the bootloader |
| /dev/         | device files (pseudo files) |
| /etc/         | host specific system configuration |
|               | (not binary programs, only scripts)
| /home/        | user home directories |
| /lib/         | essential shared libraries |
| /media/       | mount point for removable media |
|               | (usually used for system mounted media) |
| /mnt/         | mount point for temporary mounted filesystem |
|               | (usually used for user mounted media) |
| /opt/         | add on application software packages |
| /sbin/        | system binaries |
| /srv/         | data for services provided by this system |
| /tmp/         | temporary files |
| /usr/         | (multi-)user utilities and applications |
| /usr/bin/     |  |
| /usr/include/ |  |
| /usr/lib/     |  |
| /usr/sbin/    |  |
| /var/         | variable files, that change in size and content |
| /var/cache/   |  |
| /var/log/     |  |
| /var/spool/   |  |
| /var/tmp/     |  |
| /root/        | home directory for the root user |
| /proc/        | virtual filesystem documenting kernel and process status as text files |
|               | only exists in memory, not on disk |
|               | separate directory for every process |
|               | information only gathered as needed |


![Standard unix filesystem](images/standard-unix-filesystem-hierarchy-1.webp)
source: linuxfoundation.org

## Often used directories and files

### /etc/passwd
- this file is like a phonebook for all user accounts
- each line represents one user account
```
myuser:x:50001:5001::/home/myuser:/bin/sh
```
- `myuser`: username
- `x`: password (the actual password is stored securely in `/etc/shadow`)
- `5001`: user ID
- `5001`: group ID
- `/home/myuser`: home directory
- `/bin/sh`: default shell

### /etc/shadow
- text based password file
- stores hashed passphrases for Linux user accounts