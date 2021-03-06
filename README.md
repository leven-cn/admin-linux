admin-linux
==================

Admin Linux

## STEP 0

**STEP 1**: Install [VirtualBox](http://www.virtualbox.org/) and **Guest Additions**.

**STEP 2**: Create virtual machine on VirtualBox VM.

**STEP 3**: Set VirtualBox Share (VirtualBox 4.0+)

**STEP 4**: Install Linux (Server) on VirtualBox VM.

**STEP 4**: Setup share directory on Linux (Server) guest.

```bash
sudo gpasswd -a <user> vboxsf
```

**STEP 5**: Re-Login Linux (Server).

The auto-mounted directory is mounted to `/media/sf_<share-dir>`.

For convenience, you could create a symbolic link in your home directory.

```bash
ln -s /media/sf_<share-dir> ~/.
```

**STEP 6**: Configure *NAT* + *Host-Only* network mode.

```bash
# On Linux (Server) guest
echo "" >> /etc/network/interfaces
echo "auto eth1" >> /etc/network/interfaces
echo "iface eth1 inet dhcp" >> /etc/network/interfaces
```

## User Guide

**STEP 1**: Install Git

```bash
# Debian/Ubuntu
sudo apt-get update
sudo apt-get install git
```

**STEP 2**: Setup

```bash
git config --global user.name "Li Yun"                # replace with your name
git config --global user.email leven.cn@gmail.com     # replace with your email address

cd ~                                                  # choose your own path
git clone https://github.com/leven-cn/admin-linux.git

cd admin-linux
python3 admin.py setup|quick-setup
```

**STEP 3**: Build projects

```bash
# uWSGI
python3 admin.py run-uwsgi <app-path> <address>
python3 admin.py stop-uwsgi <app-path>
python3 admin.py init-run-uwsgi <app-path> <address>
tail -f /var/log/uwsgi/<app-name>.log

# nginx
python3 admin.py enable-nginx <app-path> [<upstream-address>]
python3 admin.py disable-nginx [<app-path> <upstream-address>]
tail -f /var/log/nginx/access.log
tail -f /var/log/nginx/error.log

# doc
python admin.py doc <project-path>
```
