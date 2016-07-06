# pam_py_usb

**This is a program DESIGNED FOR OS X**

This utility allows for the use of a flash drive (or any other volume, even a partition)
to be used in place of a password

# Automatic Install
Use the .pkg inside the dmg or /build for an automatic install
View the documentation for a better undersanding of what the installer actually dies

# Manual Install
1. Compile pusb.c:
```bash
gcc -fPIC -DPIC -shared -rdynamic -o pusb.so pusb.c
```
2. Move pusb.so to /usr/lib/pam
3. Then add into /etc/pam.d/ conf files using PAM syntax
    auth       sufficient     pusb.so
   * Change sufficient to requisite to force the use of a usb and password combination
     Otherwise, sufficient allows either to authenicate
     Be sure to place the python code in the PATH for all users

---

If you aren't comfortable in the command line, or don't know much about PAM
PLEASE keep sudo -i open in terminal before modifying anything 

# Documentation
## Usage
3 python binaries are put into PATH:
###### pam_py_usb_add
###### pam_py_usb_check
###### pam_py_usb_renew

# TODO
- [ ] Per-user auth
- [ ] Trigger program (unlock screensaver?) on plug/unplug
- [ ] Clean up filenames and paths
- [x] Installer
- [ ] Uninstaller
- [ ] Linux support? (pam_usb)