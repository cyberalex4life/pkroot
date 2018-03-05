# pkroot
### Description:
Scripts and policy suite to run almost everything with visual Polkit authentification in Bash.

### Installation
#### Full installation
```
$ git clone https://github.com/cyberalex4life/pkroot.git
$ cd pkroot
$ chmod a+x runwithpkexec pkroot
$ sudo cp org.freedesktop.policykit.pkexec.runwithpkexec.policy /usr/share/polkit-1/actions

## If "/usr/local/bin" does not exist, create it ##
$ ! [ -d "/usr/local/bin" ] && sudo mkdir -p /usr/local/bin || echo 'Folder exists'

$ sudo cp -t /usr/local/bin runwithpkexec pkroot
```
#### Just as a wrapper to run a single command with 'pkexec' in the background
For this you only need to put **pkroot** in a location from PATH variable:
```
$ chmod a+x runwithpkexec

## If "/usr/local/bin" does not exist, create it ##
$ ! [ -d "/usr/local/bin" ] && sudo mkdir -p /usr/local/bin || echo 'Folder exists'

$ sudo cp -t /usr/local/bin pkroot
```
Then run your command with
```
pkroot -d [command]
```
**Note** that only one command will work and that it needs a custom `*.policy` file placed in `/usr/share/polkit-1/actions`.

This is useful if you want to bypass ``Refusing to render service to dead parents.``

### To uninstall
```
$ sudo rm -fv /usr/local/bin/{runwithpkexec,pkroot} /usr/share/polkit-1/actions/org.freedesktop.policykit.pkexec.runwithpkexec.policy
```

### How does it work?
**runwithpkexec** acts as a wrapper or container for every command(s) that are passed by **pkroot**. To be able to pass multiple commands, one must enclose them in " " or ' ' :
```
$ pkroot 'tlp-stat -b; tlp-stat -t'
```
To be able to run successfully a program or command with polkit (aka pkexec), there must be some policy file installed (placed) in "/usr/share/polkit-1/actions", or at list this is one approach. The biggest problem is that one should create such a file for each specific program or this is time consumming and annoying.

What we're trying to achieve here is to use only one policy file every time we want to run an app as root with Polkit. To do this we need a 'mule' script that is able to contain every command we want root privileges for and that needs only one policy installed.

Here goes 'runwithpkexec' that looks like this:
```
#! /bin/bash
sh -c "$@"
```

Very simple right? So now we can do this:
```
pkexec runwithpkexec 'tlp-stat -b; tlp-stat -t'
```

To further simplify our commands, we add another container script, 'pkroot':
```
#! /bin/bash
pkexec runwithpkexec "$@"
```
Such that we only have to use a single word instead of two to run our commands with Polkit.

Some issues over different distro's suggested it would be best to execute 'runwithpkexec' using the entire installation path. that is why the actual script in this repo looks differently.

### Most importantly when you install pkroot!!!
If you want to place your scripts in other locations you must be sure

* they are marked executable,
* that 'pkroot' holds the entire path of 'runwithpkexec', especially if it is not placed in global PATH variable locations,
* that 'org.freedesktop.policykit.pkexec.runwithpkexec.policy' holds this path in '`<annotate key="org.freedesktop.policykit.exec.path">/usr/local/bin/runwithpkexec</annotate>`'.

**Note** that 'pkroot' may be placed in a different location than the  install location of 'runwithpkexec'.
