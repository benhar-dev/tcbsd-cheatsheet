# TwinCAT BSD Cheatsheet

## Disclaimer

This is a personal guide not a peer reviewed journal or a sponsored publication. We make
no representations as to accuracy, completeness, correctness, suitability, or validity of any
information and will not be liable for any errors, omissions, or delays in this information or any
losses injuries, or damages arising from its display or use. All information is provided on an as
is basis. It is the reader’s responsibility to verify their own facts.

The views and opinions expressed in this guide are those of the authors and do not
necessarily reflect the official policy or position of any other agency, organization, employer or
company. Assumptions made in the analysis are not reflective of the position of any entity
other than the author(s) and, since we are critically thinking human beings, these views are
always subject to change, revision, and rethinking at any time. Please do not hold us to them
in perpetuity.

## Major version update

```
doas pkg update -f && doas pkg upgrade
doas pkg install tcbsd-upgrade
doas tcbsd-upgrade major
shutdown -r now
```

## Operation

restart 

```
# shutdown -r now
```

## Settings

```
doas ee /etc/rc.conf
```

## Network

IP Address finding
```
# ifconfig
```

Find open listening ports

```
# sockstat -4 -l
```

## Firewall

### Stopping and Starting

```
# doas service pf stop
# doas service pf start
```

### Disable firewall

```
doas ee /etc/rc.conf
```
```
firewall_enable="NO"
```

