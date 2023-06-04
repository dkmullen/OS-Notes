Remote access

## Windows ##
- PuTTY
- SSH default port is 22
- From PS - putty.exe -ssh -dkm@<ip> 22
- plink - putty link - also for ssh (and other?) connections
- ssh is good for connecting win to linux
- for win to win, RDP - Remote Desktop Protocol - there are also RDP clients for mac/linux which allow remote access to win desktop
- mstsc.exe (Microsoft Terminal Services Client) is used to make remote connections
- Enable remote connections in This PC > Properties > Remote Settings
- To connect, type mstsc at the run box or find Remote Desktop Connections
- Or connect from cmd with more options like /admin

File transfer - putty supports scp with pscp.exe

Also, from the desktop, right click a folder > share with . choose people > etc
Then go to **File Explorer > This PC > Map network Drive**
or from the cli with net share <folderName>=<path> /grant:everyone full

net share (without args) lists all shared folders

VMs - Virtual Box - host and guests

Logging
- Event Viewer - Start Menu or eventvwr.msc
- Create Custom View on right hand side, click critical and error
last hour, windows logs

Other categories - Windows logs > system or security, etc

Service logs - track events for single applications rather than sys wide

## Linux ##
File transer with scp - secure copy between computers over ssh
scp /home/Desktop/me_file dkm@<ip>:

logging - /var/log - remember var contains files that change

The one log file that logs pretty much everything on your system is the */var/log/syslog* file. The only thing that syslog doesn't 
log by default are off events. 
  
When troubleshooting issues with user machines /var/log/syslog will usually contain the most comprehensive information 
  about your system. That should be your first stop. 

logrotate is a sys tool for cleaning up logs - can adjust the settings for how long to keep logs

Tactics - Work from the 'top' to get at root cause
- or from the bottom
- or in real time - tail -f /var/log/syslog
