# OpenSuse Install 
- Disks partitions
  - root Btrfs w/o snap
  - home Xfs
- Use KDE with packages selections 
  - fortune, gimp, nmap, glances, krita, ... 
  - Google Noto, Jetbrains, Fira, Microsofts Fonts, .... see also https://www.programmingfonts.org/

## Bash Tweaking
- Add to bash aliases `vi ~/.alias`
```bash
alias r='npm run' 
alias ll='ls -lh'
alias df='df -h'
alias cls='clear'
```
- Customize bash history [Tuto](https://www.cherryservers.com/blog/a-complete-guide-to-linux-bash-history)
Add to .bashrc
```bash
export HISTCONTROL=ignoreboth:erasedups
export HISTIGNORE='clear':'ls *':'ll *':'history*':'exit':'reboot':'zypper*'
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

## Customize git
```bash
git config --global user.name  'Carlos de Cumont'
git config --global user.email 'carlos@decumont.be'
```

## Start and Customize Samba
```bash
smbpasswd -a cdc 
```

## Customize FirewallD
```bash
firewall-cmd --get-zones
```


# KVM/QEMU Install
- Install with `yast` ! Bridge br0 will be added.
  Something buggy with KNetWorkManager so use Wicker
- Use default virtual network `192.168.122.x`
- Adjust Firewall to access local Samba Server
```bash
firewall-cmd --get-zones
firewall-cmd --zone=libvirt --list-all
firewall-cmd --zone=libvirt --list-services
firewall-cmd --zone=libvirt --permanent --add-interface virbr0
firewall-cmd --zone=libvirt --permanent --add-service samba 
systemctl restart firewalld
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
- [top](https://github.com/ClementTsang/bottom)  `sudo zypper in bottom`
- [cat](https://github.com/sharkdp/bat)  `sudo zypper in bat` 

Add to bash aliases `vi ~/.alias`
```
alias find='fd'

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



dsffd
fdsfds
fdsf
























