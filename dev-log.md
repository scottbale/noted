# August 2011 - first days at Revelytix
MONDAY

Install ubuntu 10.10 full disk installation

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

GitHub create new RSA public key, add to GitHub account
https://help.github.com/articles/generating-ssh-keys

skype

git clone clojure; build from src

* need to add repo 
dropbox: http://www.dropbox.com/downloading?os=lnx
chrome: http://www.google.com/linuxrepositories/ 

Install Leiningen (install script from github page into ~/bin/, chmod +x, add to $PATH, "lein self-install")
lein deps
lein compileDeps
lein compile
lein test
lein upgrade

Install ~/.hgrc

configure .m2 - copy settings.xml to ~/m2

emacs
M-x package-install then clojure-mode

hg clone http://www.assembla.com/revelytix-common

knoodel cert https://build.knoodel.net/maven-repo
bottom-right corner->details->export .net file, then
sudo keytool -import -alias root -file /home/scott/Downloads/gd_intermediate.crt -storepass changeit -trustcacerts -keystore /usr/lib/jvm/java-6-openjdk/jre/lib/security/cacerts
sudo keytool -import -alias cross -file /home/scott/Downloads/gd_cross_intermediate.crt -storepass changeit -trustcacerts -keystore /usr/lib/jvm/java-6-openjdk/jre/lib/security/cacerts

sudo updatedb
locate foo
locate bar

TUESDAY

* install IntelliJ idea Community edition (http://blog.kasunbg.org/2010/03/install-intellij-idea-in-linux.html) and La Clojure plugin
* Ryan demo'd SLIME and swank
* built Spyder snapshot dist, installed, began using
** read some docs
** ran some examples (see other notes)

Leiningen
* lein new project-name
* lein deps
* lein compileDeps
* lein compile
* lein dist
* lein swank

Emacs
* M-x slime-connect
* C-c C-k load/compile
* C-c M-p repl at namespace
* C-x C-e eval expr
* C-c v eval buffer
* M-. func src
* M-* or C-x b ???


WEDNESDAY

* play around with "spyder-tool demo"
* Watch over Nate's shoulder for https://www.assembla.com/spaces/revelytix-spyder/tickets/356
* did some Clojure scratch work ~/sandbox/scratch

lein test revelytix.spyder.endpoint.test-http

Clojure
* replace "if (do (" with "when(" unless there's an "else"
* "doseq" drop-in non-lazy replacement for "for"

Emacs
* paredit cheat sheet
* M-! shell command "tree"*
tw There should be a Clojure Lint called Clint
* in repl use (in-ns 'somenamespace)
* vc-mode C-x V D
* M-/ hippie complete
* M-x rgrep
** P N forward/back navigation of results
* emacs kill ring
** M-y cycle through kill ring for yank
** M-x browse-kill-ring (need to install module)

THURSDAY

* Sat in on engineering con call
* Attempting an upgrade to Ubuntu 11.04 to deal with Intel Sandybridge video card issues (see http://blogs.intel.com/technology/2011/01/sandybridge_on_linux_-_it_will.php, http://www.phoronix.com/scan.php?page=article&item=intel_snb_natty&num=1)
* lspci | grep VGA
* reading "Revelytix Spyder Native Mapping Language" doc side-by-side with spyder-tool demo

Ubuntu crash, and recover w/ 11.04 install disk (and help from Ryan)
* reinstall gnome-do, chrome, git, hg, emacs, java, dropbox, etc.

Linux tips
* Ctrl-Alt-F2 - bring up terminal [Ctrl-Alt-F1..F8 switch between terminals]
* sudo /etc/init.d/gdm restart - restart Gnome display manager

FRIDAY

install skype https://help.ubuntu.com/community/Skype
enable Canonical partners repo (use Software Center)
sudo apt-get install skype

wiki https://revelytix.servehttp.com:553/wiki/Human_Resources

sent website feedback to Paul

installed Federator, ran demo

emacs color-theme debugging (thanks Ryan)
http://blog.dskang.com/2011/05/14/fixing-the-color-theme-problem-with-the-emacs-starter-kit/

correct Federator README

MONDAY 8/29/11

keytool -list -keystore /usr/lib/jvm/java-6-openjdk/jre/lib/security/cacerts -alias root -v

sudo apt-get install tk8.5 (for wish)

Mercurial commit:
hg pull -u or hg in
hg view
hg heads
hg rebase -b 2192 -d tip
hg outgoing
hg push

TUESDAY 8/30/11

backup 
sudo apt-get install backintime-common
sudo apt-get install backintime-gnome
sudo apt-get install cryptsetup

WEDNESDAY 8/31/11

install mysql thru synaptic

TUESDAY 9/6/11

hg glog -l 5

C-A-Backspace - ubuntu restart session (recover from crash)

FRIDAY 9/9/11

Build
https://wiki.revelytix.com:553/wiki/BuildServer
ssh -p 3122 -i <build server key> -o "ServerAliveInterval=10" build@xxx.xxx.xxx.xxx
screen [-r]
jenkins@build:~/jobs/Spyder/workspace$ /usr/local/revelytix_data/lein test revelytix.spyder.tool.test-tool

Wed 9/28
              (println "<!><!><!><!> ttl")
              (clojure.stacktrace/print-stack-trace (Exception.))


(comment (def tuple {
                     :b (new-literal*
                         {:lexical "2001-01-01 01:01:01.0",
                          :datatype (java.net.URI. "http://www.w3.org/2001/XMLSchema#dateTimeStamp")}),
                     :name (new-literal* {
                                          :lexical "bill",
                                          :datatype (java.net.URI. "http://www.w3.org/2001/XMLSchema#string")})})


Monday 10/24/11
parser stuff (in repl)
revelytix.grammar.sql> 
(revelytix.parsergen.slr/output-canonical-states)
(dbg-parse "sELeCt a from b")
(apply dbg-parse *1)
all-productions

Tuesday 11/1/11
EC2 ops repl session:

; SLIME 20100404
user> 
revelytix.ops> (init)
#<AmazonEC2Client com.amazonaws.services.ec2.AmazonEC2Client@1652d654>
revelytix.ops> aws
#<AmazonEC2Client com.amazonaws.services.ec2.AmazonEC2Client@1652d654>
revelytix.ops> (describe-instances (memfn getImageId) #(.. % getState getName))
(["ami-4b4ba522" "stopped"] ["ami-5b799232" "stopped"] ["ami-56936b3f" "stopped"])
revelytix.ops> (describe-images "ami-b62ac0df" "ami-4b4ba522" "ami-56936b3f" "ami-5b799232" [:imageId :name :description])
({:description "Oracle on Ubuntu 10.04 Server 64-bit", :name "Oracle 112_P2 Ubuntu", :imageId "ami-5b799232"} {:description "Even better as now the startup script is executable. I'm a dumbass.", :name "Oracle 112_P2 WebLogic 40G Latest Aug24-2", :imageId "ami-b62ac0df"})
revelytix.ops> (clojure.pprint/pprint (describe-images "ami-b62ac0df" "ami-4b4ba522" "ami-56936b3f" "ami-5b799232" [:imageId :name :description]))
({:description "Oracle on Ubuntu 10.04 Server 64-bit",
  :name "Oracle 112_P2 Ubuntu",
  :imageId "ami-5b799232"}
 {:description
  "Even better as now the startup script is executable. I'm a dumbass.",
  :name "Oracle 112_P2 WebLogic 40G Latest Aug24-2",
  :imageId "ami-b62ac0df"})
nil
revelytix.ops> (clojure.pprint/pprint (describe-images "ami-b62ac0df" "ami-4b4ba522" "ami-56936b3f" "blahblahblah" "ami-5b799232" [:imageId :name :description]))
; Evaluation aborted.
revelytix.ops> (clojure.pprint/pprint (describe-images "ami-b62ac0df" "ami-4b4ba522" [imageId :name :description]))
; Evaluation aborted.
revelytix.ops> (clojure.pprint/pprint (describe-images "ami-b62ac0df" "ami-4b4ba522" [:imageId :name :description]))
({:description
  "Even better as now the startup script is executable.",
  :name "Oracle 112_P2 WebLogic 40G Latest Aug24-2",
  :imageId "ami-b62ac0df"})
nil
revelytix.ops> (clojure.pprint/pprint (describe-images "ami-4b4ba522" [:imageId :name :description]))
()
nil
revelytix.ops> (map (memfn getPublicDnsName) (running-instances))
("ec2-174-129-187-23.compute-1.amazonaws.com")
revelytix.ops> (terminate-running)
#<TerminateInstancesResult {TerminatingInstances: [{InstanceId: i-cb02dea8, CurrentState: {Code: 32, Name: shutting-down, }, PreviousState: {Code: 16, Name: running, }, }], }>
revelytix.ops> 

Wed 11/2/11
acpi - check battery

Thu 12/1/11
ssh tunnelling for remote Amazon EC2 mysql box
ssh -L 3360:localhost:3306 ubuntu@xxx.xx.xx.xxx
(see ~/bin/pf script for example)


xmonad
install xmonad (sudo apt-get install xmonad)
Create /usr/share/xsessions/xmonad-gnome-session.desktop
Create /usr/share/gnome-session/sessions/xmonad.session
(maybe) Create /usr/share/applications/xmonad.desktop file

Mon 4/23/12
sudo rfkill list all

export JDK_HOME=/home/scott/sandbox/sunjdk-7/jdk1.7.0

trayer --edge top --align right --SetDockType true --SetPartialStrut false --expand true --width 5 --transparent true --tint 0x0000000 --height 18 --alpha 0 &

apt-get
apt-cache

M-: (setq kill-ring nil)

Dropbox git remote steps:
http://stackoverflow.com/questions/1960799/using-gitdropbox-together-effectively
cd ~/Dropbox/git
git init --bare foo.git
cd ~/foo
git remote add origin ~/Dropbox/git/foo.git
git push -u origin master

Tue 1/22/2013

upgrading to emacs 24, building from source
(clone from github, cd into directory, then)
sudo apt-get install autoconf automake
./autogen.sh
sudo apt-get install texinfo libgtk3-dev libgif-dev libjpeg-dev
libtiff-dev libxpm-dev libtinfo-dev
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

Thu 1/24/2013

truncate long lines in a tail
tail spyder.log | cut -b 1-80

Fri 1/25/2013

grep -r -B 1 -A 80 something.something logs/spyder.log

tar -czf foo.tar.gz bar/

Fri 2/8/2013

Emacs
    M-: eval
    M-! shell command

Fri 2/12/13 grep tricks
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

2/13/13

Sys admin tools: top, htop, w, iostat, nmap, du

2/19/13

Install ssh daemon
    apt-get openssh-server
Restart
    sudo service ssh restart
ssh with X tunnelling
    ssh -X scott@your-dell-laptop
Find hostname
    ifconfig
    `hostname`.local

emacs C-O all grep occurences

2/22/13

gnome-terminal profiles
    ~/.gconf/apps/gnome-terminal/profiles/Solarized/
terminfo
    /usr/share/terminfo/
    /lib/terminfo/
emacs terminal stuff
    ~/sandbox/emacs/lisp/term/
emacs color cells
    (display-color-cells (selected-frame))
or
    (tty-display-color-cells (selected-frame))
    C-x C-e eval in scratch buffer
colors
    M-x list-colors-display
terminfo? ncurses? tput

3/1/13
create .tar.gz (gzipped) file of director(ies):
    tar -czvf archive.tar.gz foo/ bar/
extract tar
    tar -xzvf archive.tar.gz

3/7/13
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

3/13/13
Emacs global search and replace
http://emacswiki.org/emacs/DiredSearchAndReplace
    C-u M-x
    Dired listing switches: -lR
in dired mode, mark directories:
    * /
then toggle marks to mark only files
    t
(or, mark files according to regexp % m)
then do search replace regexp
    Q
accept all
    Y
In IBuffer (C-x C-b), mark all unsaved
    * u
then save all marked
    S
    
regexp search and replace "Query" with "Transform"
    M-x replace-regexp (also works in above dired steps)
    \([^a-zA-Z0-9]+\)Query+
    Ret
    \1Transform
    Ret

3/25/13
start Loom transactor:
    ~/dev/revelytix-bigdata/fabric/bin/transactor ~/dev/revelytix-bigdata/fabric/conf/transactor.properties > /dev/null &

7/29/13 getting Deech up-and-running

install: hg, mvn, lein
.hgrc
.m2/settings.xml
add Deech to big-data, common
https://www.assembla.com/spaces/revelytix-common/wiki/Build_Server section 3.3.1
clojure.complete license - lein version > 2.0.0 "include clojure-complete as a dependency in the :base profile, which we use to create the dist" -Alex
- solution: downgrade leiningen
- https://github.com/technomancy/leiningen/issues/1267 Alex logged

9/22/13 

sudo apt-get autoremove

http://artofsimplicity.co.uk/install-dropbox-on-a-headless-ubuntu-server/
~/bin/dropbox.py help
https://www.dropbox.com/help/175/en

scp .hgrc then
hg clone https://hg.assembla.com/revelytix-bigdata/
sudo apt-get install openjdk-7-jdk (hopefully has godaddy certs, for maven repo on build server - didn't work)
(needed to do import 2 godaddy cacerts steps from build server wiki page)

1/29/14

Setup Docker:

http://docs.docker.io/en/latest/installation/ubuntulinux/

    sudo sh -c "echo deb http://get.docker.io/ubuntu docker main\
    > /etc/apt/sources.list.d/docker.list"

    sudo apt-get install lxc-docker

Run hello world

    sudo docker run -i -t ubuntu /bin/bash

5/9/14

count lines of code

    scott@scott-latitude:~/dev/revelytix-bigdata/fabric/src/main/resources/public/js/rvtx$ find . -name "*.html" -o -name "*.js" | xargs wc -l

6/6/14 tag loom release

    hg tag -m "tag Loom 2.2.0 release (re #3557)" 2.2.0

6/9/14 update java cacerts - relevant directories

    ~/bin/java
    /usr/lib/jvm/
    /etc/ssl/certs/java/cacerts

see

    https://www.assembla.com/spaces/revelytix-common/wiki/Build_Server#3.3.1_go_daddy_certificates

tried it:

    ~$ keytool -import -alias godaddy_intermediate_g2 -file ~/Downloads/gdig2.crt -trustcacerts -keystore /etc/ssl/certs/java/cacerts
    Enter keystore password:  

password

    <%=revelytix-jdk-certs%>

7/7/14 Wordpress

'home' and 'site' urls can be stored either in `wp-config.php` (`WP_HOME`, `WP_SITEURL`) or in mysql `kwcoc_options` table with `option_name` column of `home` and `siteurl`.

Assembla->Git Migration

    git --version
    hg paths
    mv .hgignore .gitignore

instructions https://www.assembla.com/code/revelytix-bigdata/git/repo/instructions

cloned 'fast-export', did the export

    git clone git://repo.or.cz/fast-export.git

cloned fresh copy of hg repo

    mkdir revelytix-bigdata-prime
    hg clone https://hg.assembla.com/revelytix-bigdata revelytix-bigdata-prime/

made new empty repo

    mkdir revelytix-bigdata-git
    cd revelytix-bigdata-git
    git init

did export

    ../fast-export/hg-fast-export.sh -r ../revelytix-bigdata-prime/

generate and upload ssh key to assembla profile

added remote to git repo

    git remote add assembla git@git.assembla.com:revelytix-bigdata.git

push

    git push --all assembla

Watch all three Godfather films

Use 'https'

    https://git.assembla.com/revelytix-bigdata.git

(instead of 'git')

    git@git.assembla.com:revelytix-bigdata.git


7/9/14
 
list processes by user

    ps -ef

7/12/14 xargs example

    find . -name "*.bak" -print0 | xargs -0 -I file mv file ~/old.files

7/14/14 git config

    git config --global -l
    git config --local -l

7/16/14

backup Jenkins, Nexus

    /usr/local/revelytix_data/hudson-backups
    /usr/local/revelytix_data/sonatype-work/nexus

tar/gzip director(ies)

    tar czvf foo.tar.gz folder1 folder2... folderN

## 8/5/14

change Grub default

    fgrep menuentry /boot/grub/grub.cfg
    sudo zile /etc/default/grub 
    sudo update-grub

## 8/8/14 setup new ubuntu vm

Ubuntu git maintainers team has a PPA

    sudo add-apt-repository ppa:git-core/ppa
    sudo apt-get update
    sudo apt-get install git
    
emacs 24 ppa

    sudo add-apt-repository ppa:cassou/emacs
    sudo apt-get update
    sudo apt-get install emacs24 emacs24-el emacs24-common-non-dfsg
    
git checkout files from other branches into index

    git checkout <branch_name> -- <paths>

install git
install emacs24
git clone dotfiles (some tweaking)
install zile, openjdk-7-jdk, maven2, tree, lein (2.2 initially), 

emacs right Meta key not working: http://www.emacswiki.org/emacs/PuTTY#toc7

emacs color theme not displaying

configure test git repo
build server cert, import to java keystore

    curl -v -u [QID] http://[location of cert file]
    sudo keytool -import -alias build_self_signed -keystore /etc/ssl/certs/java/cacerts -file foo.cert

cant figure out `wget` or `curl` from wiki page to vm due to
authentication failure. Resorting to `scp` from desktop.

git clone Alex's test repo
git clone assembla repo; test lein compile
working on public key authentication w/ putty

## 8/19/14

ubuntu node ppa https://launchpad.net/~chris-lea/+archive/ubuntu/node.js

    sudo apt-add-repository ppa:chris-lea/node.js
    sudo apt-get install nodejs

(nodejs includes npm)

    sudo npm install -g grunt-cli

## 8/23/14 minecraft mods

minecraft forge-src

    ./gradlew setupDecompWorkspace --refresh-dependencies

### server

install installer http://files.minecraftforge.net/

    wget http://files.minecraftforge.net/maven/net/minecraftforge/forge/1.7.10-10.13.0.1208/forge-1.7.10-10.13.0.1208-installer.jar

run installer (headless)

    java -jar forge-1.7.10-10.13.0.1208-installer.jar --installServer

run universal jar (note manifest file defines a classpath, dependent on libraries/ folder)

    java -jar forge-1.7.10-10.13.0.1208-universal.jar

## 8/28/14

rpm - list files in a package

    rpm -qlp foo.rpm

use different leiningen version: just edit header of `~/bin/lein` and re-run. It will install to `~/.lein/self-installs/~.

command line `if`

    if id -u foo; then echo "true"; else echo "false"; fi

display the return status of most recently executed foreground command or pipeline:

    echo $?

## 9/3/14 - rpm

build

    lein do clean, with-profile rpm-generic install

install

    sudo rpm -v -i target/foo.rpm

check install

    rpm -q foo

uninstall

    rpm -e foo

## 9/8/14

hdfs

    sudo -u hdfs hadoop fs -mkdir /data
    sudo -u hdfs hadoop fs -mkdir /data/sources

Copy Folders from Local Directories to HDFS Source Directory

    sudo -u hdfs hadoop fs -copyFromLocal /home/bob/data/sources/aviz_datasets /data/sources

single path

    sudo -u hdfs hadoop fs -put <localfile> <hdfspath>


## 9/13/14 putty notes

### create Windows shortcut

modify properties; shortcut should read something like

    "C:\Program Files (x86)\putty\putty.exe" -load foo

### for terminal emacs

http://www.emacswiki.org/emacs/PuTTY

change term colors 

    Connection->Data->Terminal-type string = "xterm-256color"

make both 'alt' keys be 'meta' keys; regedit

    Windows Registry Editor Version 5.00
    [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layout]
    "Scancode Map"=hex:00,00,00,00,00,00,00,00,03,00,00,00,1d,00,3a,00,38,00,38,e0,00,00,00,00

Explained here http://smallvoid.com/article/winnt-scancode-map.html

* first 8 bytes are headers
* `03 00 00 00` indicates 3 entries in map (including null entry)
* `1d 00 3a 00` makes right Alt key work as a meta key
* `38 00 38 e0` makes Caps Lock key another Ctrl key
* null entry at the end

## 9/25/14

Gnu screen quick notes

Config file: `~/.screenrc`

| task          | binding     |
| ------------- | ----------- |
| split         | `M-S`       |
| rename window | `M-A`       |
| focus region  | `M-tab`     |
| window list   | `M-"`       |

## 9/29/14

Needed to use `eval` to start ssh-agent, something to do with env variable(s) that running `ssh-agent` exports, and which `ssh-add` needs.

    eval `ssh-agent -s`
    ssh-add foo

## 10/5/14

post JSON via curl

    curl -X POST -H "Content-Type: application/json" -d @file.json http://hostname:8080/api/v1/foo/bar

reboot vm

    sudo reboot

## 10/28/14

Emacs tramp mode

    C-x C-f /ssh:user@hostname:/path/to/file

## 10/29/14

Logged in as root, create a user account for myself (RHEL)

    useradd -m -s /bin/bash sbale
    mkdir /home/sbale/.ssh
    ...
    chown -R sbale:sbale /home/sbale/.ssh/
    chmod 600 /home/sbale/.ssh/*
    passwd -S sbale

See process using port `8083`

    sudo netstat -tapen | grep 8083
    ps -fp [pid]

## 11/3/14

    sudo hadoop fs -rm -f -r -skipTrash /user/foo

## 11/13/14

### rejigger linux users & groups

UIDs and GIDs

    id -u username
    id -g username
    id -G username
    getent group [gid]
    getent group [groupname]
    getent passwd [id]
    getent passwd [uname]

change user UID, GID

    usermod -u [new uid] -g [new gid]
    groupmod -g [new gid]

new user foo

    groupadd -g 2112 foo
    useradd -g 2112 -u 5150 foo

modify user foo

    groupmod -g 2112 foo
    usermod -u 5150 -g 2112 foo
