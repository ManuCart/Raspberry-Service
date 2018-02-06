
````
    ┌───┐             ┐                   ┌──┐          ┌─┬─┐     ┐           ┐
    │   │             │                   │  │ .        │ │ │ .   │     .     │
    ├──┬┘ ┌─┐ ┌─┐ ┌─┐ ├─┐ ┌─┐ ┌┐ ┌┐ ┐ ┌   ├──┘ ┐        │ │ │ ┐ ┌─┤ ┬─┐ ┐ ┌─┬ ├─┐ ┼
    │  │  ┌─┤ └─┐ │ │ │ │ ├─┘ │  │  │ │   │    │   ──   │ │ │ │ │ │ │ │ │ │ │ │ │ │
    ┴  └┘ └─┴ └─┘ ├─┘ └─┘ ┴─┘ ┴  ┴  └─┤   ┴    ┴        ┴   ┴ ┴ └─┴ ┴ ┴ ┴ └─┤ ┴ ┴ └┘
                  ┴        ──────Menu─┘                     ──────Commander─┘
````
Use Midnight Commander (mc) user menu with tmux for friendly way do some jobs and related stuff

```bash
sudo apt-get install mc sshpass tmux
git clone git@github.com:ManuCart/Raspberry-Pi.git ~/rpi
cd rpi
.\rescue
```


## Requirements
### Raspbian
https://www.raspberrypi.org/downloads/raspbian/
Download and Install
http://sourceforge.net/projects/win32diskimager/files/Archive/win32diskimager-v0.9-binary.zip/download
Download Raspbian lite
https://downloads.raspberrypi.org/raspbian_lite_latest
Download putty and write

```bash
start /MAX putty -ssh pi@192.168.0.1
```

### Configuration

```bash
sudo raspi-config
```

+ Expand Filesystem
+ Internationalisation Options
  - Change Locale add [*] fr_FR.UTF-8 UTF-8
  - Default locale for the system environement : fr_FR.UTF-8
  - Change Timezone with Geographic area : Europe and Time zone : Paris
+ Enable Camera
+ Overclock
  - Medium
+ Reboot

```bash
sudo apt-get install mc tmux rsync exiv2
sudo ln -sf bash /bin/sh
```

### Updating
```bash
sudo apt-get autoremove
sudo apt-get update
sudo apt-get -y upgrade
sudo rpi-update
```

### Ssh
```bash
mkdir ~/.ssh
cd ~/.ssh
ssh-keygen -t rsa -b 4096 -N '' -C pi@raspberry
mv id_rsa.pub authorized_keys
sudo chmod 600 authorized_keys
cat << EOF | sudo tee -a /etc/ssh/sshd_config
PermitRootLogin no
AuthorizedKeysFile /home/pi/.ssh/authorized_keys
PasswordAuthentication no
Match Address 127.0.0.1,192.168.0.0/24
    PasswordAuthentication yes
EOF
sudo service ssh restart
```

### Samba
```bash
sudo apt-get -y install samba samba-common-bin
cat << EOF | sudo tee -a /etc/samba/smb.conf
[HDD]
comment = Raspberry Pi Hard Drive
path = /media/hdd
valid users = @users
force group = users
create mask = 0660
directory mask = 0771
read only = no
EOF
sudo service smbd restart
sudo smbpasswd -a pi
```

### Node.js
https://nodejs.org

```bash
wget https://nodejs.org/dist/v8.3.0/node-v8.3.0-linux-armv6l.tar.gz
sudo tar -xvf node-v8.3.0-linux-armv6l.tar.gz --strip 1 -C /usr/local
rm node-v8.3.0-linux-armv6l.tar.gz
```

### Go Lang
https://golang.org/dl/
arm
```bash
wget https://storage.googleapis.com/golang/go1.8.1.linux-armv6l.tar.gz
sudo tar -xvf go1.8.1.linux-armv6l.tar.gz -C /usr/local
rm go1.8.1.linux-armv6l.tar.gz
sudo mkdir /opt/go
sudo chown -R pi:pi /opt/go
cat << '!' >> ~/.bashrc
export GOROOT=/usr/local/go
export GOPATH=/opt/go
export PATH="$PATH:$GOROOT/bin:$GOPATH/bin"
!
source ~/.bashrc
```
linux64
```bash
wget https://storage.googleapis.com/golang/go1.8.3.linux-amd64.tar.gz
sudo tar -xvf go1.8.3.linux-amd64.tar.gz -C /usr/local
rm go1.8.3.linux-amd64.tar.gz
sudo mkdir /opt/go
sudo chown -R <user>:<user> /opt/go
cat << '!' >> ~/.bashrc
export GOROOT=/usr/local/go
export GOPATH=/opt/go
export PATH="$PATH:$GOROOT/bin:$GOPATH/bin"
!
source ~/.bashrc
```

### Python
```bash
sudo apt-get install python-pip python-dev
sudo pip install --upgrade pip
```

### Python3
```bash
sudo apt-get -y install python3-pip
sudo pip3 install --upgrade pip3
```

## License

MIT License

Copyright (c) 2014-2018 Emmanuel CHARETTE

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
