# pam_py_usb

# This is a program DESIGNED FOR OS X

This utility allows for the use of a flash drive (or any other volume, even a partition)
to be used in place of a password

# Automatic Install
Use the .pkg inside the dmg or /build for an automatic install

# Manual Install
Compile pusb.c:
    gcc -fPIC -DPIC -shared -rdynamic -o pusb.so pusb.c
and place in /usr/lib/pam
Then add into /etc/pam.d/ conf files using PAM syntax
    auth       sufficient     pusb.so
Change sufficient to requisite to force the use of a usb and password combination
Otherwise, sufficient allows either to authenicate
Be sure to place the python code in the PATH for all users

---
- a
If you aren't comfortable in the command line, or don't know much about PAM
PLEASE keep sudo -i open in terminal before modifying anything 
-

