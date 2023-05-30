**Windows:**
- Domain - A network of computers, users, files, etc. that are added to a central db
- Computer management tool
-- In the management tool under System Tools: Task scheduler, event viewer (logs), shared folders, performance (monitoring tools), device manager;
-- Also Storage and Services and applications
-- For power users, this management tool is a more effecient way to manage the computer than the regular settings menus
-- Local Users and Groups - appears in the CMTool in Pro and Student versions, but not in home
-- PowerShell cmds for the above: Get-LocalUser, Get-LocalGroup, Get-LocalGroupMember Administrators

UAC - User Access Control - prevents unauthorized changes

- net user dkmullen 'new_pwd' - change pw in ps - or, better: net user dkm * (which causes net to pause and let you enter a hidden pwd) - Using this to change pwds for other is ok, but the admin knows the pwd. Better yet to have the user change pwd at next login...
- net user dkm /logonpasswordchange:yes
- net user cindy * /add - to add a user
- net user cindy pa$sw0rd /add /logonpasswordchange:yes - one command to create a user, set temp pw, require change at login
- net user andrea /del or Remove-LocalUser andrea - both remove an account

Permissions
- ACL DACL (Discretionary ACL), SACL (system ACL, tells windows to make a log whenever someone accesses a file/folder)
- Read, Read and Execute, List folder contents (an alias for read and execute on a directory), Write (files, but alos make subdirectories, write files to them), Modify (inc r x w), Full control
- Windows has an explicit DENY permission flag, which takes precedence over ALLOW; if a user is part of a group with permissions to read, you can use DENY to exclude them anyway.
- icacls 'C:Vacation Pictures\' /grant 'Everyone:(OI)(CI)(R)' - Gives permission to all to access the Vacation Pics - the quotes around the permissions are to tell powershell to ignore parantheses as icacls is really a cmd commmand. Everyone is a group that includes all users, including guests. An alternative would be to use the 'Authenticated Users' group
- icacls 'C:Vacation Pictures\' /grant 'Everyone:(OI)(CI)(R)'
- icacls 'C:Vacation Pictures\' /grant 'Authenticated Users:(OI)(CI)(R)'
- icacls 'C:Vacation Pictures\' /remove 'Everyone:(OI)(CI)(R)'
- The above sets permissions for everyone, then after consideration, sets them for Auth Users and removes them for everyone

An access control list (ACL) is a list of access control entries (ACE). Each ACE in an ACL identifies a trustee and specifies the access rights allowed, denied, or audited for that trustee. The security descriptor for a securable object can contain two types of ACLs: a DACL and an SACL.

A discretionary access control list (DACL) identifies the trustees that are allowed or denied access to a securable object. When a process tries to access a securable object, the system checks the ACEs in the object's DACL to determine whether to grant access to it. If the object doesn't have a DACL, the system grants full access to everyone. If the object's DACL has no ACEs, the system denies all attempts to access the object because the DACL doesn't allow any access rights. The system checks the ACEs in sequence until it finds one or more ACEs that allow all the requested access rights, or until any of the requested access rights are denied.

icacls Desktop - returns... DESKTOP-KKI2LKK\dkmul:(I)(OI)(CI)(F) F = full access, I = inherit; also Object Inherit and Container Inherit, which means if I create objects / containers on the Desktop, they will inherit permissions

Simple permissions which we have been using are actually groups of Special Permissions - for example READ combines List Folder/Read Data, Read Attributes and Read Extended Attributes

**Linux**
- Has admins and regular users but also the root or super user
- sudo
- sudo su - (substitute user, which defaults to root if you don't specify; essentially logging in as root, to keep from typing sudo)
- cat /etc/groups to see members of groups - sudo:x:27:dkmullen - group name:pwd (encrypted, defaults to root):uid:username
- cat /etc/passwd to see users - root:x:0:0:root:/root:/bin/bash - username:pwd:uid
- passwd dkmullen - to change pwd - pwds are encrypted and stored in etc/shadow
- sudo passwd -e dkmullen (sets pw to immediately expire (-e) and user has to change at next logon
- sudo useradd juan 
- sudo userdelete juan

Permissions:
- r w x - Permissions have ten bits -rwxrw-r-- First bit is type, dash means regular file (d = dir), then owner, group, all (or is it user, group, other?)
- chmod u+x me_file - adds executable permission to user (use a - to remove it)
- chmod u+rx adds r and x
- chmod ugo+rx adds r and x to u, g, others

The above is symbolic format. Below is numerical format (4 = r, 2 = w, 1 = x)
- chmod 754 - owner = 7 or 4+2+1 or rwx; group = rw, o = read
- sudo chown fletch my_file
- sudo chgrp my_group my_file - changes the group the file belongs to

Special Permission:
- ls -l /usr/bin/passwd reveals permissions of -rwsr-xr-x - The s where owner execute should be means setuid and allows us to run the file with the permissions that the owner has. In this case, root is the owner but I can run this file to set my own password
- set the SetUID bit with chmod u+s or chmod 4755 (prepend the 4)
- SetGID with g+s or 2755
- Sticky bit - allows anyone to write  to file or folder but only root can delete indicated with a t at the end - drwxrwxrwt
- Set sticky bit with chmod +t my_folder/ or chmod 1755 my_folder/

