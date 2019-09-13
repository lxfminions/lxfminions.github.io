---
layout: post
title: Linux notes
categories: [it]
tags: [Linux]
date: 2019/09/13
---

## PackageManage
### Ubuntu
1. List the installed software packages on Ubuntu
<div class="terminal" markdown="1">
`$ sudo apt list --installed`
</div>

2. Completely remove intalled software includes configuration
<div class="terminal" markdown="1">
`$ sudo apt purge <package-name>`
</div>

3. [apt vs apt-get difference](https://itsfoss.com/apt-vs-apt-get-difference)

4. Debian operating system ==> dpkg packaging system: from high to low 
  - `apt`, most used command in `apt-get` and `apt-cache`
  - `apt-get` && `apt-cache` etc. upgrade, search, install dependenies and more
  - `dpkg`, install && remove && build(dpkg-deb)
  - `dpkg-deb`, build && manipulate archive(.deb)

5. APT: Advaced Package Tool  &  apt: high-level command line interface

### Arch Linux

## SSH
1. Generate a pair key: `ssh-keygen -t ras -b 4096 -C "comment@example.com"`
2. Start `ssh-agent`: `eval "$(ssh-agent -s)"`
3. Add keys to `ssh-agent`: `ssh-add ~/.ssh/id_rsa`
4. Verified: `ssh -T git@github.com`

## Mic
1. `blockdev --getbsz /dev/sdb10`: get the size of a block in bytes
2. File type isn't of accosiation with postfix in Linux.
3. ps: `pts` is a abbreviation of **pseudoterminal devices**
4. Install google font on ubuntu 18.04 LTS:
    1. `cd /usr/share/fonts`
    2. `sudo mkdir googlefonts`
    3. `unzip -d . ~/Downloads/fonts.zip`
    4. `sudo chmod -R --reference=opentype googlefonts`
    5. `sudo fc-cache -fv`: register fonts
    6. `fc-match font_name`: check if font installed
