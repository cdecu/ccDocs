# OpenSuse Install 
- Disks partitions
  - root Btrfs w/o snap
  - home Xfs
- Use KDE with packages selections 
  - fortune, gimp, nmap, glances, krita, ... 
  - Google Noto, Jetbrains, Fira, Microsofts Fonts, .... see also https://www.programmingfonts.org/
- Download and Install Chrome, Visual Studio Code, Spotify, ...


## Tweek Swap, ....
```bash
# we dont want to swap much if at all possible
echo 1 > /proc/sys/vm/swappiness
# hopefully better multitasking I/O performance
echo 20 > /proc/sys/vm/dirty_ratio
# Try to keep at least 100MB of free RAM at all times
echo 100000 > /proc/sys/vm/min_free_kbytes
# Default 100 - try more aggressively to reclaim inodes, etc from cache
echo 160 > /proc/sys/vm/vfs_cache_pressure
```

## Install NodeJS
- Download latest source  `configure ; make`
- Install in a root console (ctrl+alt+F1) `make install`
- Use npm [custom global dir](https://docs.npmjs.com/resolving-eacces-permissions-errors-when-installing-packages-globally)
```bash
mkdir ~/.npm-global
npm config set prefix '~/.npm-global'
vi .profile  add export PATH=~/.npm-global/bin:$PATH
```
- Customize some settings
```bash
npm config set depth 0
npm config set init-author-name 'Carlos de Cumont'
npm config set init-author-email carlos@decumont.be
npm completion >> ~/.bashrc
```

## Install and Customize git
```bash
sudo zypper in git
git config --global user.name  'Carlos de Cumont'
git config --global user.email 'carlos@decumont.be'
```

## Install and Customize Samba
As I use samba to share folders between all Windows VMs, I need to add all the windows users ...
```bash
smbpasswd -a cdc 
```

## FirewallD
Just using the default install !
```bash
firewall-cmd --get-zones
systemctl restart firewalld
```

# KVM/QEMU Install
- Install with `yast` ! Bridge br0 will be added.
  Sometime it can be buggy with KNetWorkManager so use Wicker
If bridge br0 not added ( see [configure netw bridge](https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/8/html/configuring_and_managing_networking/configuring-a-network-bridge_configuring-and-managing-networking#configuring-a-network-bridge-by-using-nmcli_configuring-a-network-bridge) )
- Add firewall_backend=iptables in /etc/libvirt/network.conf
```bash
nmcli c show
nmcli c add type bridge ifname br0 con-name br0
nmcli c modify enp3s0 master br0
nmcli c modify bridge0 connection.autoconnect-slaves 1
```
- Use default NAT virtual network `192.168.122.x`  
- Adjust Firewall to access local Samba Server
```bash
firewall-cmd --get-zones
firewall-cmd --zone=libvirt --list-all
firewall-cmd --zone=libvirt --list-services
firewall-cmd --zone=libvirt --permanent --add-interface virbr0
firewall-cmd --zone=libvirt --permanent --add-service samba 
systemctl restart firewalld
```
- adjust permission 
```bash
usermod -a -G libvirt <my-username>
```
- From time to time compress qcow2 files
```bash
export TMPDIR=/bigdisk/
mv Codotra.qcow2  Codotra.qcow2.old
virt-sparsify --compress Codotra.qcow2.old Codotra.qcow2
rm Codotra.qcow2.old
```

# Docker install
- Use yast and follown [Tuto](https://en.opensuse.org/User:Tsu2/docker-build-tutorial-1)
```bash
zypper in docker
systemctl start docker
systemctl enable docker
usermod -a -G docker <my-username>
```
- see also 
  - https://en.opensuse.org/User:Tsu2/docker-enter
  - http://jpetazzo.github.io/2014/06/23/docker-ssh-considered-evil/
  - https://store.docker.com/images/python?tab=description
  - https://en.opensuse.org/User:Tsu2/docker-build-tutorial-1

# Add Alternative Cmd Line Tools
- [tldr](https://github.com/dbrgn/tealdeer)  `sudo zypper in tealdeer`
- [find](https://github.com/sharkdp/fd)  `sudo zypper in fd`
- [sed](https://github.com/chmln/sd)  `sudo zypper in sd`
- [du](https://github.com/bootandy/dust)  `sudo zypper in dust`
- [diff](https://github.com/dandavison/delta)  `sudo zypper in git-delta`
- [ls](https://github.com/eza-community/eza)  `sudo zypper in eza`
- [top](https://github.com/ClementTsang/bottom)  `sudo zypper in bottom` `btm`
- [cat](https://github.com/sharkdp/bat)  `sudo zypper in bat` 

## Bash Tweaking
- Add to bash aliases `vi ~/.alias`
```bash
alias r='npm run' 
alias ll='ls -lh'
alias dir='eza -lh --octal-permissions'
alias df='df -h'
alias cls='clear'
alias find='fd'
```
- Customize bash history [Tuto](https://www.cherryservers.com/blog/a-complete-guide-to-linux-bash-history)
  Add to .bashrc
```bash
export HISTCONTROL=ignoreboth:erasedups
export HISTIGNORE='clear':'ls *':'ll*':'history*':'exit':'reboot':'zypper*':'..':'cd ~'
```


# Add Python Alternatives
```bash
sudo update-alternatives --install /usr/bin/python python /usr/bin/python2.7 2
sudo update-alternatives --install /usr/bin/python python /usr/bin/python3.11 3
sudo update-alternatives --install /usr/bin/python python /usr/bin/python3.12 4
sudo update-alternatives --config python
```

# Add JAVA Alternatives
```bash
sudo update-alternatives --install 
sudo update-alternatives --config java
```

# Install Visual Studio Code [see](https://linuxiac.com/how-to-install-vs-code-on-opensuse-leap-tumbleweed/)
```bash
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo zypper addrepo https://packages.microsoft.com/yumrepos/vscode vscode
sudo zypper refresh
sudo zypper install code
code 
```
