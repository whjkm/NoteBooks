## WSL Ubuntu 20.04 LTS upgrate to 22.04 LTS

show ubuntu release version before upgrade.
```
lsb_release -a

No LSB modules are available.
Distributor ID: Ubuntu
Description:    Ubuntu 20.04.6 LTS
Release:        20.04
Codename:       focal
```

prompt set to `lts`.
```
cat /etc/update-manager/release-upgrades

# Default behavior for the release upgrader.

[DEFAULT]
# Default prompting and upgrade behavior, valid options:
#
#  never  - Never check for, or allow upgrading to, a new release.
#  normal - Check to see if a new release is available.  If more than one new
#           release is found, the release upgrader will attempt to upgrade to
#           the supported release that immediately succeeds the
#           currently-running release.
#  lts    - Check to see if a new LTS release is available.  The upgrader
#           will attempt to upgrade to the first LTS release available after
#           the currently-running one.  Note that if this option is used and
#           the currently-running release is not itself an LTS release the
#           upgrader will assume prompt was meant to be normal.
Prompt=lts
```

update command

```
sudo apt update

sudo apt upgrade -y

sudo do-release-upgrade
```

after upgrate
```
No LSB modules are available.
Distributor ID: Ubuntu
Description:    Ubuntu 22.04.3 LTS
Release:        22.04
Codename:       jammy
```


## resourse
https://dowww.spencerwoo.com/2-cli/2-1-terminal.html#windows-terminal

https://learn.microsoft.com/zh-cn/windows/wsl/wsl-config#wslconfig