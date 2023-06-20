# TwinCAT BSD Cheatsheet

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

