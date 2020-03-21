# pam_py_usb

#### Please note, this software is broken, unmaintaned, and will likely royally break your system.
#### The code is left online for educational purposes.  Questions about methodology are welcome in my e-mail.

**This is a program DESIGNED FOR OS X**

This utility allows for the use of a flash drive (or any other volume, even a partition)
to be used in place of a password

Please note in OS X authenication windows, just press enter in the password field to log in when the correct key is attached

# Automatic Install
Use the .dmg inside /release or .pkg in /pkg/build for an automatic install
View the documentation for a better undersanding of what the installer actually does

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
   This can be done using a bash loop such as:
``` bash
for i in /etc/pam.d/*
do
        echo "auth       sufficient     pusb.so" > $i.new
        cat $i >> $i.new
        mv $i.new $i
        # rm $i.new
        # sed -i '1d' $i
done
echo [] > /etc/pam_py_usb_keys
```

---

If you aren't comfortable in the command line, or don't know much about PAM
PLEASE keep sudo -i open in terminal before modifying anything 

# Documentation
## Usage
3 python binaries are put into PATH:
### # pam_py_usb_add
This command creates a USB key based on whats monted in /Volumes/
### $ pam_py_usb_check
This command does not require root, and allows you to see if there are valid authenication keys mounted, as well as ran whenever you su or sudo
### # pam_py_usb_renew
Run this as root to invalidate all current keys

# TODO
- [ ] Per-user auth
- [ ] Trigger program (unlock screensaver?) on plug/unplug
- [ ] Clean up filenames and paths
- [x] Installer
- [ ] Uninstaller
- [ ] Linux support? (pam_usb)
- [ ] Fix blank login box on Apple windows
