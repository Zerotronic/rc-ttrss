# rcttrss
A TTRSS-Update-Daemon RC script for FreeBSD

## How to use:

1. Create a user to run the rcttrss update daemon (eg. ttrss) and invite him to the apache group (eg. www)
```
# adduser
Username: ttrss
Full name: RCTTRSS Update Daemon User
Uid (Leave empty for default):
Login group [ttrss]:
Login group is ttrss. Invite ttrss into other groups? []: www
Login class [default]:
Shell (sh csh tcsh zsh nologin) [sh]: 
Home directory [/home/ttrss]:
Home directory permissions (Leave empty for default):
Use password-based authentication? [yes]:
Use an empty password? (yes/no) [no]:
Use a random password? (yes/no) [no]:
Enter password:
Enter password again:
Lock out the account after creation? [no]:
Username   : ttrss
Password   : ****
Full Name  : RCTTRSS Update Daemon User
Uid        : 1002
Class      :
Groups     : ttrss www
Home       : /home/ttrss
Shell      : /bin/sh
Locked     : no
OK? (yes/no): yes
adduser: INFO: Successfully added (ttrss) to the user database.
Add another user? (yes/no): no
Goodbye!
#
```

2. Download `rcttrss` file and move it to your `/usr/local/etc/rc.d/` folder
```
# fetch https://github.com/Zerotronic/rc-ttrss/raw/master/rcttrss
# mv rcttrss /usr/local/etc/rc.d/
# chown root:wheel /usr/local/etc/rc.d/rcttrss
# chmod 555 /usr/local/etc/rc.d/rcttrss && chmod ug+x /usr/local/etc/rc.d/rcttrss
```

3. Enable the service in `/etc/rc.conf`
```
# echo '# Enable RCTTRSS-Update-daemon' >> /etc/rc.conf
# echo 'rcttrss_enable="YES"' >> /etc/rc.conf
```

4. If your tt-rss Database is not local (i.e. on the same machine) then do the following
```
# echo 'rcttrss_local_db="NO"' >> /etc/rc.conf
```

5. Open rcttrss file with an editor and check that all the parameters are correct for your tt-rss installation. (e.g. ttrss_dir is the path where your tt-rss installation lives. rcttrss_db_type is the type of database your tt-rss installation uses, mysql or postgresql, etc.)

6. Make folders needed by tt-rss update_daemon2.php writable
```
# chmod -R 775 [tt-rss_dir]/cache/images
# chmod -R 775 [tt-rss_dir]/cache/upload
# chmod -R 775 [tt-rss_dir]/cache/export
# chmod -R 775 [tt-rss_dir]/cache/js
# chmod -R 775 [tt-rss_dir]/feed-icons
# chmod -R 775 [tt-rss_dir]/lock
```

7. The update daemon of tt-rss requires that the php executable is in /usr/bin so if it is not there create a symbolic link
```
# ln -s /usr/local/bin/php /usr/bin/php
```

8. Start the service
```
# service rcttrss start
```

9. You can control the service using the following commands.
```
# service rcttrss start   (Will start the service)
# service rcttrss stop    (Will gracefully stop the service, i.e. wait for all the pids to return after collecting their data)
# service rcttrss stopnow (Will SIGKILL the service and all the pids regardless if they were in the middle of a task)
# service rcttrss status  (Will return running status and pid of the service as well as child and grandchild pids)
# service rcttrss restart (Will gracefully restart the service)
```
