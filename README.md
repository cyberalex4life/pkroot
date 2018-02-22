# pkroot
### Description:
Scripts and policy suite to run almost everything with visual Polkit authentification in Bash.

### Installation
```
$ git clone https://github.com/cyberalex4life/pkroot.git
$ cd pkroot
$ chmod a+x runwithpkexec pkroot
$ sudo cp org.freedesktop.policykit.pkexec.runwithpkexec.policy /usr/share/polkit-1/actions

## If "/opt/scripts" does not exist, create it ##
$ ! [ -d "/opt/scripts" ] && sudo mkdir -p /opt/scripts || echo 'Folder exists'

$ sudo cp -t /opt/scripts runwithpkexec pkroot
```

### To uninstall
```
$ sudo rm -fv /opt/scripts/{runwithpkexec,pkroot} /usr/share/polkit-1/actions/org.freedesktop.policykit.pkexec.runwithpkexec.policy
```
