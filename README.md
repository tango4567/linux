# Wellcome to the Linux commands collections

<br>
This repository is collection of multiple linux commands.

# Install phpmyadmin
`sudo apt-get install phpmyadmin`

* For staring phpmyadmin you need to add all line at the bottom of apache2.conf file*
I'm using geany editor here

`sudo geany /etc/apache2/apache2.conf`
Add following line at the end of this file

#### Include /etc/phpmyadmin/apache.conf


# Check mysql running port id and ip
`netstat -tlnp`


# How to uninstall and install apache in Ubuntu.

Actully I'm getting following problem with solution with terminal output:

"This page isn’t working
localhost is currently unable to handle this request.
HTTP ERROR 500"

I will discussie more about this error later. 

First we see how to uninstall apache2

(1) `apt-get remove packagename`

will remove the binaries, but not the configuration or data files of the package packagename. It will also leave dependencies installed with it on installation time untouched.

(2) `apt-get purge packagename` or `apt-get remove --purge packagename`

will remove about everything regarding the package packagename, but not the dependencies installed with it on installation. Both commands are equivalent.

(4) `apt-get autoremove`

removes orphaned packages, i.e. installed packages that used to be installed as an dependency, but aren't any longer. Use this after removing a package which had installed dependencies you're no longer interested in.

(5) `aptitude remove packagename` or `aptitude purge packagename (likewise)`

will also attempt to remove other packages which were required by packagename on but are not required by any remaining packages. Note that aptitude only remembers dependency information for packages that it has installed. 

`sudo apt-get autoremove` 

 `Reading package lists... Done
 Building dependency tree
 Reading state information... Done
 0 upgraded, 0 newly installed, 0 to remove and 14 not upgraded.
 3 not fully installed or removed.
 Need to get 0 B/12.1 MB of archives.
 After this operation, 0 B of additional disk space will be used.
 dpkg: error processing package geoip-database-extra (--configure):
 package geoip-database-extra is not ready for configuration
 cannot configure (current status 'half-installed')
 Setting up runit (2.1.2-3ubuntu1) ...
 start: Unable to connect to Upstart: Failed to connect to socket /com/ubuntu/upstart: Connection refused
 dpkg: error processing package runit (--configure):
 subprocess installed post-installation script returned error exit status 1
 dpkg: dependency problems prevent configuration of git-daemon-run:
 git-daemon-run depends on runit; however:
 Package runit is not configured yet.
 dpkg: error processing package git-daemon-run (--configure):
 dependency problems - leaving unconfigured
 No apport report written because the error message indicates its a followup error from a previous failure.
 Errors were encountered while processing:
 geoip-database-extra
 runit
 git-daemon-run
 E: Sub-process /usr/bin/dpkg returned an error code (1)`

**For Solving above problem**
`sudo apt-get autoremove`

`Reading package lists... Done
Building dependency tree       
Reading state information... Done
E: The package geoip-database-extra needs to be reinstalled, but I can't find an archive for it.`

**For Solving above problem**
Start with

`sudo dpkg --remove --force-all hl1440lpr`

If that fails ...

# become root
`sudo -i`
`cd /var/lib/dpkg/info`
`rm -rf hl1440lpr*`

`dpkg --remove --force-remove-reinstreq hl1440lpr`

exit
Confirm apt-get is fixed

# should return no errors
`sudo apt-get update`

# Got Solution For geoip
  `sudo add-apt-repository universe`

# Then i run this command
`sudo apt-get install geoip-database-extra`

`Reading package lists... Done
Building dependency tree       
Reading state information... Done
geoip-database-extra is already the newest version (20160408-1).
0 upgraded, 0 newly installed, 0 to remove and 8 not upgraded.
3 not fully installed or removed.
Need to get 0 B/12.1 MB of archives.
After this operation, 0 B of additional disk space will be used.
Do you want to continue? [Y/n] y
dpkg: error processing package geoip-database-extra (--configure):
 package geoip-database-extra is not ready for configuration
 cannot configure (current status 'half-installed')
Setting up runit (2.1.2-3ubuntu1) ...
start: Unable to connect to Upstart: Failed to connect to socket /com/ubuntu/upstart: Connection refused
dpkg: error processing package runit (--configure):
 subprocess installed post-installation script returned error exit status 1
dpkg: dependency problems prevent configuration of git-daemon-run:
 git-daemon-run depends on runit; however:
  Package runit is not configured yet.

dpkg: error processing package git-daemon-run (--configure):
 dependency problems - leaving unconfigured
No apport report written because the error message indicates its a followup error from a previous failure.
                                                                                                          Errors were encountered while processing:
 geoip-database-extra
 runit
 git-daemon-run
E: Sub-process /usr/bin/dpkg returned an error code (1)
`

# Then i run this command
`sudo apt-get purge runit`

`Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following package was automatically installed and is no longer required:
  fgetty
Use 'sudo apt autoremove' to remove it.
The following packages will be REMOVED:
  git-daemon-run* runit*
0 upgraded, 0 newly installed, 2 to remove and 8 not upgraded.
3 not fully installed or removed.
Need to get 0 B/12.1 MB of archives.
After this operation, 1,162 kB disk space will be freed.
Do you want to continue? [Y/n] y
(Reading database ... 421221 files and directories currently installed.)
Removing git-daemon-run (1:2.7.4-0ubuntu1.3) ...
Purging configuration files for git-daemon-run (1:2.7.4-0ubuntu1.3) ...
warning: /etc/sv/git-daemon: unable to open supervise/ok: file does not exist
warning: /etc/sv/git-daemon/log: unable to open supervise/ok: file does not exist
warning: /etc/sv/git-daemon: unable to open supervise/ok: file does not exist
warning: /etc/sv/git-daemon/log: unable to open supervise/ok: file does not exist
rmdir: failed to remove '/var/log/git-daemon': No such file or directory
Removing runit (2.1.2-3ubuntu1) ...
stop: Unable to connect to Upstart: Failed to connect to socket /com/ubuntu/upstart: Connection refused
Removing SV inittab entry...
Purging configuration files for runit (2.1.2-3ubuntu1) ...
Processing triggers for man-db (2.7.5-1) ...
dpkg: error processing package geoip-database-extra (--configure):
 package geoip-database-extra is not ready for configuration
 cannot configure (current status 'half-installed')
Errors were encountered while processing:
 geoip-database-extra
E: Sub-process /usr/bin/dpkg returned an error code (1)
`
# Then i run this command 
`  sudo apt-get --purge remove libc6-dev-i386 libc6-dev-x32 gcc-5-multilib gcc-multilib`

`Reading package lists... Done
Building dependency tree       
Reading state information... Done
Package 'gcc-multilib' is not installed, so not removed
Package 'gcc-5-multilib' is not installed, so not removed
Package 'libc6-dev-i386' is not installed, so not removed
Package 'libc6-dev-x32' is not installed, so not removed
The following package was automatically installed and is no longer required:
  fgetty
Use 'sudo apt autoremove' to remove it.
0 upgraded, 0 newly installed, 0 to remove and 8 not upgraded.
1 not fully installed or removed.
Need to get 0 B/12.1 MB of archives.
After this operation, 0 B of additional disk space will be used.
dpkg: error processing package geoip-database-extra (--configure):
 package geoip-database-extra is not ready for configuration
 cannot configure (current status 'half-installed')
Errors were encountered while processing:
 geoip-database-extra
E: Sub-process /usr/bin/dpkg returned an error code (1)
`

# Then i run this command 
`sudo dpkg --remove --force-remove-reinstreq --dry-run libgfortran3:amd64`

`dpkg: dependency problems prevent removal of libgfortran3:amd64:
 libgfortran-5-dev:amd64 depends on libgfortran3 (>= 5.4.0-6ubuntu1~16.04.9).
 liblapack3 depends on libgfortran3 (>= 4.6).
 python-scipy depends on libgfortran3 (>= 4.6); however:
  Package libgfortran3:amd64 is to be removed.
 libhdf5-10:amd64 depends on libgfortran3 (>= 4.3).

dpkg: error processing package libgfortran3:amd64 (--remove):
 dependency problems - not removing
Errors were encountered while processing:
 libgfortran3:amd64`

# Then i run this command 

`sudo apt-get --purge remove libc6-dev-i386 libc6-dev-x32 gcc-5-multilib gcc-multilib`

`Reading package lists... Done
Building dependency tree       
Reading state information... Done
Package 'gcc-multilib' is not installed, so not removed
Package 'gcc-5-multilib' is not installed, so not removed
Package 'libc6-dev-i386' is not installed, so not removed
Package 'libc6-dev-x32' is not installed, so not removed
The following package was automatically installed and is no longer required:
  fgetty
Use 'sudo apt autoremove' to remove it.
0 upgraded, 0 newly installed, 0 to remove and 8 not upgraded.
1 not fully installed or removed.
Need to get 0 B/12.1 MB of archives.
After this operation, 0 B of additional disk space will be used.
dpkg: error processing package geoip-database-extra (--configure):
 package geoip-database-extra is not ready for configuration
 cannot configure (current status 'half-installed')
Errors were encountered while processing:
 geoip-database-extra
E: Sub-process /usr/bin/dpkg returned an error code (1)`


# Finally I Ran 
`sudo apt-get install --reinstall geoip-database-extra`

`Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following package was automatically installed and is no longer required:
  fgetty
Use 'sudo apt autoremove' to remove it.
0 upgraded, 0 newly installed, 1 reinstalled, 0 to remove and 8 not upgraded.
1 not fully installed or removed.
Need to get 0 B/12.1 MB of archives.
After this operation, 0 B of additional disk space will be used.
Selecting previously unselected package geoip-database-extra.
(Reading database ... 421146 files and directories currently installed.)
Preparing to unpack .../geoip-database-extra_20160408-1_all.deb ...
Unpacking geoip-database-extra (20160408-1) over (20160408-1) ...
Setting up geoip-database-extra (20160408-1) ...
`

# Then udate Command
`sudo apt-get update`

# Then i run this command 
` sudo apt autoremove` 

`Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following packages will be REMOVED:
  fgetty
0 upgraded, 0 newly installed, 1 to remove and 8 not upgraded.
After this operation, 64.5 kB disk space will be freed.
Do you want to continue? [Y/n] y
(Reading database ... 421145 files and directories currently installed.)
Removing fgetty (0.7-1) ...
Processing triggers for man-db (2.7.5-1) ...`

# Then I tried with following command
`sudo apt-get install geoip-database-extra`

`Reading package lists... Done
Building dependency tree       
Reading state information... Done
geoip-database-extra is already the newest version (20160408-1).` <-- i already have newest version
`0 upgraded, 0 newly installed, 0 to remove and 8 not upgraded.`


# Finally I Solved my Problem with geoip


