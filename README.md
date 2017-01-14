# rc-ttrss
A TTRSS-Update-Daemon RC script for FreeBSD

## How to use:

1. Create a user to run the tt-rss update daemon (eg. ttrss) and invite him to the apache group (eg. www)
```
# adduser
Username: ttrss
Full name: TTRSS Update Daemon User
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
Full Name  : TTRSS Update Daemon User
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

2. Download `ttrss` file and move it to your `/usr/local/etc/rc.d/` folder
```
# fetch https://github.com/Zerotronic/rc-ttrss/raw/master/ttrss
# mv ttrss /usr/local/etc/rc.d/
# chown root:wheel /usr/local/etc/rc.d/ttrss
# chmod 755 /usr/local/etc/rc.d/ttrss && chmod ug+x /usr/local/etc/rc.d/ttrss
```

3. Enable the service in `/etc/rc.conf`
```
# echo '# Enable TTRSS-Update-daemon' >> /etc/rc.conf
# echo 'ttrss_enable="YES"' >> /etc/rc.conf
```

4. Start the service
```
# service ttrss start
```
