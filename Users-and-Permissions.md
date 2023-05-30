Windows:
Computer management tool
Domain - A network of computers, users, files, etc. that are added to a central db
In the management tool under System Tools: Task scheduler, event viewer (logs), shared folders, performance (monitoring tools), device manager;
Also Storage and Services and applications
For power users, this management tool is a more effecient way to manage the computer than the regular settings menus
Local Users and Groups - appears in the CMTool in Pro and Student versions, but not in home
PowerShell cmds for the above: Get-LocalUser, Get-LocalGroup, Get-LocalGroupMember Administrators
UAC - User Access Control - prevents unauthorized changes
net user dkmullen 'new_pwd' - change pw in ps - or, better: net user dkm * (which causes net to pause and let you enter a hidden pwd) - Using this to change pwds for other is 
ok, but the admin knows the pwd. Better yet to have the user change pwd at next login...
net user dkm /logonpasswordchange:yes
net user cindy * /add - to add a user
net user cindy pa$sw0rd /add /logonpasswordchange:yes - one command to create a user, set temp pw, require change at login
net user andrea /del or Remove-LocalUser andrea - both remove an account

Linux
Has admins and regular users but also the root or super user
sudo
sudo su - (substitute user, which defaults to root if you don't specify; essentially logging in as root, to keep from typing sudo)
cat /etc/groups to see members of groups - sudo:x:27:dkmullen - group name:pwd (encrypted, defaults to root):uid:username
cat /etc/passwd to see users - root:x:0:0:root:/root:/bin/bash - username:pwd:uid
passwd dkmullen - to change pwd - pwds are encrypted and stored in etc/shadow
sudo passwd -e dkmullen (sets pw to immediately expire (-e) and user has to change at next logon
sudo useradd juan 
sudo userdelete juan
