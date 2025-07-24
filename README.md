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

## 🚀 Update and Upgrades

### Major version update

```bash
doas pkg update -f && doas pkg upgrade
doas pkg install tcbsd-upgrade
doas tcbsd-upgrade major
shutdown -r now
```

#### Post-upgrade Cleanup (Recommended)
This is a recommended step once the upgrade has completed, and you have verified that they system is working. 

```bash
# First, delete the old restore point to free up space.
# You will be prompted to select a restore point interactively.
# IMPORTANT: Select the one named exactly like: upgrade-backup-<your timestamp>
doas restorepoint destroy

# Now we clean up the old boot environment.
# This is usually called "default", and must be removed before renaming.
doas bectl destroy default

# Check your available boot environments to find the new one.
# Look for something like "upgrade-2025-07-24T09:22:50Z"
bectl list

# Rename the upgraded boot environment to "default"
# This is important — many system tools expect a boot environment named "default"
# If you skip this step, future upgrades or restore operations will fail
doas bectl rename upgrade-<timestamp> default

# You can now reboot into a clean system state.
shutdown -r now
```

#### Jumping multiple major versions

To upgrade across multiple major versions (e.g. 12 → 13 → 14), you must repeat the entire upgrade process for each version step:

1. Perform the major upgrade (tcbsd-upgrade major).
2. Reboot into the new boot environment.
3. Verify system functionality.
4. Follow the post-upgrade cleanup steps.


## ⚙️ Operation

### Restart the System

```bash
shutdown -r now
```

---

## 🛠️ Settings

Edit `rc.conf`:

```bash
doas ee /etc/rc.conf
```

---

## 🌐 Network

### Find IP Address

```bash
ifconfig
```

### Find Open Listening Ports

```bash
sockstat -4 -l
```

---

## 🔥 Firewall

### Start/Stop PF Firewall

```bash
doas service pf stop
doas service pf start
```

### Disable Firewall on Boot

Edit `rc.conf`:

```bash
doas ee /etc/rc.conf
```

Set the following line:

```
firewall_enable="NO"
```


