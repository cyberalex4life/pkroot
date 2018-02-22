# pkroot
##### Description:
Scripts and policy suite to run almost everything with visual Polkit authentification in Bash.

### Installation:
```
$ git clone https://github.com/cyberalex4life/pkroot.git
$ cd pkroot
$ chmod a+x runwithpkexec pkroot
$ sudo cp org.freedesktop.policykit.pkexec.runwithpkexec.policy /usr/share/polkit-1/actions

## If "/usr/local/bin" does not exist, create it ##
$ ! [ -d "/usr/local/bin" ] && sudo mkdir -p /usr/local/bin || echo 'Folder exists'

$ sudo cp -t /usr/local/bin runwithpkexec pkroot
```

##### To uninstall
```
$ sudo rm -fv /usr/local/bin/{runwithpkexec,pkroot} /usr/share/polkit-1/actions/org.freedesktop.policykit.pkexec.runwithpkexec.policy
```

### How does it work?
