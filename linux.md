# LINUX

## Basic

    uname -a
    lsb_release -d
    cat /proc/meminfo
    cat /proc/cpuinfo
    df -h
    fdisk -l
    hdparm -i /dev/device (for example sda1, hda3...)

alt-F2 launches application
make Caps Lock key another ctrl key System->Preferences->Keyboard Layouts Options "Ctrl Key position"

    sudo apt-get install
    git
    hg
    emacs
    maven2
    openjdk-6-jdk
    dropbox*
    google-chrome-stable*
    tree
    vim
    
need to add repo
dropbox: http://www.dropbox.com/downloading?os=lnx
chrome: http://www.google.com/linuxrepositories/ 

## screen

    screen

screen rejoin

    screen -r
    
create new screen

    Ctrl-a c
    
toggle next screen

    Ctrl-a n

screenrc

    echo "escape ^]]" > .screenrc
    
ping localhost at interval of 10 sec

    ping -i 10 localhost

locate

    sudo updatedb
    locate foo

bring up terminal [Ctrl-Alt-F1..F8 switch between terminals]

    Ctrl-Alt-F2 - 

restart Gnome display manager

    sudo /etc/init.d/gdm restart

ubuntu restart session (recover from crash)

    C-A-Backspace

## xmonad

install xmonad (sudo apt-get install xmonad)
Create

    /usr/share/xsessions/xmonad-gnome-session.desktop
    /usr/share/gnome-session/sessions/xmonad.session
    /usr/share/applications/xmonad.desktop (maybe?)

    trayer --edge top --align right --SetDockType true --SetPartialStrut false --expand true --width 5 --transparent true --tint 0x0000000 --height 18 --alpha 0 &


Dropbox git remote steps: http://stackoverflow.com/questions/1960799/using-gitdropbox-together-effectively

    cd ~/Dropbox/git
    git init --bare foo.git
    cd ~/foo
    git remote add origin ~/Dropbox/git/foo.git
    git push -u origin master

upgrading to emacs 24, building from source (clone from github, cd into directory, then)

    sudo apt-get install autoconf automake
    ./autogen.sh
    sudo apt-get install texinfo libgtk3-dev libgif-dev libjpeg-dev libtiff-dev libxpm-dev libtinfo-dev
    ./configure --with-x-toolkit=gtk
    make
    src/emacs -Q    <-- test
    sudo make install

terminal only (amazon aws microinstance):

    sudo apt-get install texinfo libtinfo-dev ncurses-dev
    ./configure --without-x

Wed 1/23/2013
Use different JDK:
edit ~/.bashrc, set $JDK_HOME e.g.

    export JDK_HOME=/home/scott/sandbox/sunjdk-7/jdk1.7.0
    export JDK_HOME=/usr/lib/jvm/java-7-openjdk

set java in path

    ln -s /usr/lib/jvm/java-7-openjdk/jre/bin/java ~/bin/java
    
relaunch shell

    bash

truncate long lines in a tail
    tail spyder.log | cut -b 1-80

    grep -r -B 1 -A 80 something.something logs/spyder.log

    tar -czf foo.tar.gz bar/

grep tricks
# lines before/after a match
    grep -r -B 1 -A 80 something.something logs/spyder.log
# pattern is fixed string, match only whole line
    grep -Fx "a whole line" file.log
# remove dupes
    grep yadda yadda yadda | sort | uniq
# truncate lines
    grep yadda yadda yadda | cut -b 1-10

append to file

    >> 

Sys admin tools: top, htop, w, iostat, nmap, du

create .tar.gz (gzipped) file of director(ies):
    tar -czvf archive.tar.gz foo/ bar/
extract tar
    tar -xzvf archive.tar.gz

port forwarding script:

    #!/bin/sh
    HOST=ec2-107-21-140-138.compute-1.amazonaws.com
    exec ssh -i ~/dev/revelytix-spyder/spyder-testing.pem -o ServerAliveInterval=10 ubuntu@$HOST -L 3360:localhost:3306

update ubuntu JDK:

    sudo update-alternatives --config java ;; don't do this, do below instead

http://askubuntu.com/questions/141791/is-there-a-way-to-update-all-java-related-alternatives

    update-alternatives --get-selections | grep java
    /usr/sbin/update-java-alternatives -l
    sudo apt-get install icedtea-7-plugin
    sudo /usr/sbin/update-java-alternatives -s java-1.7.0-openjdk-amd64

3/26/13

    /etc/resolv.conf
    # OpenDNS
    nameserver 208.67.222.222
    nameserver 208.67.220.220

4/1/13

    DON'T hand-edit /etc/resolv.conf
    nslookup www.example.com
    sudo resolvconf-u
    sudo service network-manager restart

    sudo poweroff
    sudo reboot
    
go back to login screen

    alt + shift + q

apt (Advanced Packaging Tool package manager) notes

check package 'foo' availablility

update, upgrade

    sudo apt-get update
    sudo apt-get upgrade --dry-run
    sudo apt-get dist-upgrade
    
search

    apt-cache showpkg foo
    apt-cache search foo

see files installed for a package 'foo'

    dpkg-query -L foo
    
find what process is using a port (precede all with `sudo`)

    netstat -tulpn | grep 80
    ls -l /proc/<pid>/exe
    fuser 80/tcp

cp Music -> Important
diff and cp commands:

    diff -qr temp1/ temp2/
    cp -nRv temp1/ temp2/ > report.txt

but instead of temp2, target directory is:

    /Volumes/Important/Music/ALL/

update default editor

    sudo update-alternatives --config editor

## package managers

Guide to CLI package managers: `apt`, `yum`, `zypper`

Package managers per dist

* Ubuntu - apt
* RHEL - yum
* SUSE -
* centos - yum

Note: `repoquery` is a `yum` util:

    yum install yum-utils

See installed repos:

    apt-cache policy |grep http |awk '{print $2 $3}' |sort -u
    /etc/apt/sources.list, sources.list.d/
    yum repolist
    /etc/yum.repos.d/
    zypper lr [-d] [-u]

Add repo:

    apt-add-repository url
    curl http://repo.url/foo.repo | sudo tee /etc/yum.repos.d/foo.repo > /dev/null
    sudo wget http://repos.fedorapeople.org/repos/dchen/apache-maven/epel-apache-maven.repo \
         -O /etc/yum.repos.d/epel-apache-maven.repo    
    zypper ar -f url

remove repo:

    apt-add-repository -r url

update|refresh installed repos:

    apt-get update
    zypper refresh

upgrade

    apt-get [upgrade [--dry-run]|dist-upgrade]

Search for package:

    apt-cache search expr
    yum search expr
    zypper search expr

Search for installed package:

    apt-cache policy [pkgname]
    dpkg-query -l [expr]
    yum list installed pkg
    zypper search --installed pkg

See package details:

    apt-cache showpkg pkg
    yum info pkg
    zypper info pkg

Install package:

    apt-get install pkg
    yum install pkg
    zypper install pkg

Install package non-interactive:

    apt-get
    yum
    zypper install --non-interactive pkg

See package dependencies|requirements:

    apt-cache depends pkg
    repoquery --requires pkg
    zypper

Remove package:

    apt-get purge
    yum remove pkg
    zypper

See package installed contents:

    dpkg-query -L pkg
    repoquery --list pkg
    zypper

create new repo out of directory containing .rpm's

    zypper ar -t plaindir -n "My local directory of RPM's" /opt/foo/rpm "my-foo"
