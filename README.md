# Install Ubuntu in WSL 2

## Install WSL and Ubuntu
```powershell
wsl --install
```

## Install the GNOME Desktop
```powershell
sudo apt update && sudo apt upgrade -y
```

```powershell
sudo apt install ubuntu-desktop gnome-shell gnome-terminal -y
```

## Enable Remote Access
### Install the RDP Server
```powershell
sudo apt install xrdp -y
```
### Configure the System
```powershell
sudo adduser xrdp ssl-cert
```
```powershell
echo "gnome-session" > ~/.xsessionrc
```
```powershell
sudo /etc/init.d/xrdp start
```
### Find Your Ubuntu IP Address
```powershell
hostname -I
```

## Modify the `xrdp` Startup Script
```powershell
sudo nano /etc/xrdp/startwm.sh
```
```
# BEFORE:
test -x /etc/X11/Xsession && exec /etc/X11/Xsession
exec /bin/sh /etc/X11/Xsession

# AFTER:
unset DBUS_SESSION_BUS_ADDRESS
unset XDG_RUNTIME_DIR
gnome-session
# test -x /etc/X11/Xsession && exec /etc/X11/Xsession
# exec /bin/sh /etc/X11/Xsession
```
```powershell
sudo /etc/init.d/xrdp restart
```
