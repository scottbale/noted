# August 2011 - first days at Revelytix

## MONDAY

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

need to add repo 
* dropbox: http://www.dropbox.com/downloading?os=lnx
* chrome: http://www.google.com/linuxrepositories/ 

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

knoodel cert https://build.knoodel.net/maven-repo bottom-right corner->details->export .net file, then

    sudo keytool -import -alias root -file /home/scott/Downloads/gd_intermediate.crt -storepass changeit -trustcacerts -keystore /usr/lib/jvm/java-6-openjdk/jre/lib/security/cacerts
    sudo keytool -import -alias cross -file /home/scott/Downloads/gd_cross_intermediate.crt -storepass changeit -trustcacerts -keystore /usr/lib/jvm/java-6-openjdk/jre/lib/security/cacerts
    sudo updatedb
    locate foo
    locate bar

## TUESDAY

* install IntelliJ idea Community edition (http://blog.kasunbg.org/2010/03/install-intellij-idea-in-linux.html) and La Clojure plugin
* Ryan demo'd SLIME and swank
* built Spyder snapshot dist, installed, began using
  * read some docs
  * ran some examples (see other notes)

Leiningen
    lein new project-name
    lein deps
    lein compileDeps
    lein compile
    lein dist
    lein swank

Emacs
    M-x slime-connect
    C-c C-k load/compile
    C-c M-p repl at namespace
    C-x C-e eval expr
    C-c v eval buffer
    M-. func src
    M-or C-x b ???


## WEDNESDAY

* play around with "spyder-tool demo"
* Watch over Nate's shoulder for https://www.assembla.com/spaces/revelytix-spyder/tickets/356
* did some Clojure scratch work ~/sandbox/scratch

        lein test revelytix.spyder.endpoint.test-http

Clojure
* replace `if (do (` with `when(` unless there's an `else`
* `doseq` drop-in non-lazy replacement for `for`

Emacs
* paredit cheat sheet
* M-! shell command "tree"*
tw There should be a Clojure Lint called Clint
* in repl use (in-ns 'somenamespace)
* vc-mode C-x V D
* M-/ hippie complete
* M-x rgrep
  * P N forward/back navigation of results
* emacs kill ring
  * M-y cycle through kill ring for yank
  * M-x browse-kill-ring (need to install module)

## THURSDAY

* Sat in on engineering con call
* Attempting an upgrade to Ubuntu 11.04 to deal with Intel Sandybridge video card issues (see http://blogs.intel.com/technology/2011/01/sandybridge_on_linux_-_it_will.php, http://www.phoronix.com/scan.php?page=article&item=intel_snb_natty&num=1)
* lspci | grep VGA
* reading "Revelytix Spyder Native Mapping Language" doc side-by-side with spyder-tool demo

Ubuntu crash, and recover w/ 11.04 install disk (and help from Ryan)
* reinstall gnome-do, chrome, git, hg, emacs, java, dropbox, etc.

Linux tips
* Ctrl-Alt-F2 - bring up terminal [Ctrl-Alt-F1..F8 switch between terminals]
* restart Gnome display manager:

        sudo /etc/init.d/gdm restart - restart Gnome display manager

## FRIDAY

install skype https://help.ubuntu.com/community/Skype
enable Canonical partners repo (use Software Center)

    sudo apt-get install skype

wiki https://revelytix.servehttp.com:553/wiki/Human_Resources

sent website feedback to Paul

installed Federator, ran demo

emacs color-theme debugging (thanks Ryan)
http://blog.dskang.com/2011/05/14/fixing-the-color-theme-problem-with-the-emacs-starter-kit/

correct Federator README

## MONDAY 8/29/11

keytool -list -keystore /usr/lib/jvm/java-6-openjdk/jre/lib/security/cacerts -alias root -v

    sudo apt-get install tk8.5 (for wish)

Mercurial commit:
    hg pull -u or hg in
    hg view
    hg heads
    hg rebase -b 2192 -d tip
    hg outgoing
    hg push

## TUESDAY 8/30/11

backup 
    sudo apt-get install backintime-common
    sudo apt-get install backintime-gnome
    sudo apt-get install cryptsetup

## WEDNESDAY 8/31/11

install mysql thru synaptic

## TUESDAY 9/6/11

    hg glog -l 5

C-A-Backspace - ubuntu restart session (recover from crash)

## FRIDAY 9/9/11

Build
https://wiki.revelytix.com:553/wiki/BuildServer

    ssh -p 3122 -i <build server key> -o "ServerAliveInterval=10" build@xxx.xxx.xxx.xxx
    screen [-r]
    jenkins@build:~/jobs/Spyder/workspace$ /usr/local/revelytix_data/lein test revelytix.spyder.tool.test-tool

## Wed 9/28
    (println "<!><!><!><!> ttl")
    (clojure.stacktrace/print-stack-trace (Exception.))


    (comment (def tuple {
                     :b (new-literal*
                         {:lexical "2001-01-01 01:01:01.0",
                          :datatype (java.net.URI. "http://www.w3.org/2001/XMLSchema#dateTimeStamp")}),
                     :name (new-literal* {
                                          :lexical "bill",
                                          :datatype (java.net.URI. "http://www.w3.org/2001/XMLSchema#string")})})


## Monday 10/24/11

parser stuff (in repl)

    revelytix.grammar.sql> 
    (revelytix.parsergen.slr/output-canonical-states)
    (dbg-parse "sELeCt a from b")
    (apply dbg-parse *1)
    all-productions

## Tuesday 11/1/11

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

## Wed 11/2/11

acpi - check battery

## Thu 12/1/11

ssh tunnelling for remote Amazon EC2 mysql box

    ssh -L 3360:localhost:3306 ubuntu@xxx.xx.xx.xxx
    
(see ~/bin/pf script for example)


### xmonad

install xmonad (`sudo apt-get install xmonad`)
Create `/usr/share/xsessions/xmonad-gnome-session.desktop`
Create `/usr/share/gnome-session/sessions/xmonad.session`
(maybe) Create `/usr/share/applications/xmonad.desktop` file

## Mon 4/23/12

    sudo rfkill list all

    export JDK_HOME=/home/scott/sandbox/sunjdk-7/jdk1.7.0

    trayer --edge top --align right --SetDockType true --SetPartialStrut false --expand true --width 5 --transparent true --tint 0x0000000 --height 18 --alpha 0 &

    apt-get
    apt-cache

    M-: (setq kill-ring nil)

Dropbox git remote steps: http://stackoverflow.com/questions/1960799/using-gitdropbox-together-effectively

    cd ~/Dropbox/git
    git init --bare foo.git
    cd ~/foo
    git remote add origin ~/Dropbox/git/foo.git
    git push -u origin master

## Tue 1/22/2013

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

## Wed 1/23/2013

Use different JDK:
edit ~/.bashrc, set $JDK_HOME e.g.

    export JDK_HOME=/home/scott/sandbox/sunjdk-7/jdk1.7.0
    export JDK_HOME=/usr/lib/jvm/java-7-openjdk
    
set java in path

    ln -s /usr/lib/jvm/java-7-openjdk/jre/bin/java ~/bin/java
    
relaunch shell

    bash

## Thu 1/24/2013

truncate long lines in a tail

    tail spyder.log | cut -b 1-80

## Fri 1/25/2013

    grep -r -B 1 -A 80 something.something logs/spyder.log

    tar -czf foo.tar.gz bar/

## Fri 2/8/2013

Emacs
    M-: eval
    M-! shell command

## Fri 2/12/13 grep tricks

* lines before/after a match

        grep -r -B 1 -A 80 something.something logs/spyder.log

* pattern is fixed string, match only whole line

        grep -Fx "a whole line" file.log

* remove dupes

        grep yadda yadda yadda | sort | uniq
        
* truncate lines

        grep yadda yadda yadda | cut -b 1-10

append to file

    >> 

## 2/13/13

Sys admin tools: top, htop, w, iostat, nmap, du

## 2/19/13

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

## 2/22/13

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

## 3/1/13

create .tar.gz (gzipped) file of director(ies):

    tar -czvf archive.tar.gz foo/ bar/
    
extract tar

    tar -xzvf archive.tar.gz

## 3/7/13

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

## 3/13/13

Emacs global search and replace http://emacswiki.org/emacs/DiredSearchAndReplace

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

## 3/25/13

start Loom transactor:

    ~/dev/revelytix-bigdata/fabric/bin/transactor ~/dev/revelytix-bigdata/fabric/conf/transactor.properties > /dev/null &

## 7/29/13

getting Deech up-and-running

* install: hg, mvn, lein
* .hgrc
* .m2/settings.xml
* add Deech to big-data, common
* https://www.assembla.com/spaces/revelytix-common/wiki/Build_Server section 3.3.1
* clojure.complete license - lein version > 2.0.0 "include clojure-complete as a dependency in the :base profile, which we use to create the dist" -Alex
  * solution: downgrade leiningen
  * https://github.com/technomancy/leiningen/issues/1267 Alex logged

## 9/22/13 

    sudo apt-get autoremove

http://artofsimplicity.co.uk/install-dropbox-on-a-headless-ubuntu-server/

    ~/bin/dropbox.py help
    
https://www.dropbox.com/help/175/en

scp .hgrc then

    hg clone https://hg.assembla.com/revelytix-bigdata/
    sudo apt-get install openjdk-7-jdk (hopefully has godaddy certs, for maven repo on build server - didn't work)
    
(needed to do import 2 godaddy cacerts steps from build server wiki page)

## 1/29/14

Setup Docker:

http://docs.docker.io/en/latest/installation/ubuntulinux/

    sudo sh -c "echo deb http://get.docker.io/ubuntu docker main\
    > /etc/apt/sources.list.d/docker.list"

    sudo apt-get install lxc-docker

Run hello world

    sudo docker run -i -t ubuntu /bin/bash

## 5/9/14

count lines of code

    scott@scott-latitude:~/dev/revelytix-bigdata/fabric/src/main/resources/public/js/rvtx$ find . -name "*.html" -o -name "*.js" | xargs wc -l

## 6/6/14 tag loom release

    hg tag -m "tag Loom 2.2.0 release (re #3557)" 2.2.0

## 6/9/14 update java cacerts - relevant directories

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

## 7/7/14 Wordpress

'home' and 'site' urls can be stored either in `wp-config.php`
(`WP_HOME`, `WP_SITEURL`) or in mysql `kwcoc_options` table with
`option_name` column of `home` and `siteurl`.

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


## 7/9/14
 
list processes by user

    ps -ef

## 7/12/14 xargs example

    find . -name "*.bak" -print0 | xargs -0 -I file mv file ~/old.files

## 7/14/14 git config

    git config --global -l
    git config --local -l

    git config --local user.email "<my work email address>"

## 7/16/14

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

replaced by?

    https://launchpad.net/~ubuntu-elisp/+archive/ppa.
    
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

## 8/28/14

rpm - list files in a package

    rpm -qlp foo.rpm

use different leiningen version: just edit header of `~/bin/lein` and
re-run. It will install to `~/.lein/self-installs/~.

command line `if`

    if id -u foo; then echo "true"; else echo "false"; fi

display the return status of most recently executed foreground command
or pipeline:

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

examine file metadata

    rpm -qp foo.rpm --qf "%{name} %{url}\n"

see all possible metadata tags

    rpm --querytags
    rpm --querytags | xargs -I tag rpm -qp foo.rpm --qf "tag: %{tag}\n"

List contents of RPM package

    rpm -qlp package.rpm

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
| close splits  | `M-Q`       |
| rename window | `M-A`       |
| focus region  | `M-tab`     |
| window list   | `M-"`       |
| copy mode     | `M-[`       |

## 9/29/14

Needed to use `eval` to start ssh-agent, something to do with env
variable(s) that running `ssh-agent` exports, and which `ssh-add`
needs (`env | grep SSH_`)

    eval `ssh-agent -s`
    ssh-add foo

7/15 p.s.

    env | grep SSH_A | awk '{print "export " $0}' > ~/ssh_agent

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
    
or Mac OS X

    sudo lsof -n -i4TCP:8083 | grep LISTEN
    sudo lsof -i -n -P | grep TCP | grep LISTEN

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

(w/o id)

    groupadd foo
    useradd -g foo foo

(`adduser` perl script, delegates to `useradd`)

modify user foo

    groupmod -g 2112 foo
    usermod -u 5150 -g 2112 foo

add user to group

    usermod -a -G groupName userName

remove user

    userdel foo

what groups is user member of?

    groups username
    id username

## 12/4/14

truncate lines returned by `grep` by piping through `cut`

    grep whatever | cut -c1-170

## 12/24/14

yum package manager

    yum | more
    yum list installed emacs*
    yum repolist
    reposync
    yum info hadoop-hdfs

    /etc/yum.repos.d/

    yum upgrade foo

    yum install yum-utils
    repoquery --list packagename

compare with zypper

    zypper search --installed emacs*
    zypper se -i emacs*
    zypper info hadoop-hdfs

## 1/5/15

SUSE Linux equivalent to `yum` is `yast2` or `zypper`

## 1/7/15

cider-repl-set-ns

    C-c M-n

## 1/19/15

git push select commit to remote branch `2.3.x`:

    git push origin 2.3.x^^:2.3.x
    git push origin 235a3sd:2.3.x

git, find commit with `blarg` in commit message

    git log --grep="blarg"

Assuming a commit `a21bf32` is found, see what (local and remote)
branches it's in:

    git branch -a --contains a21bf32

## 2/10/15

show disk usage

    df -h

disk usage

    du -h /path/to

disk usage with grand total

    du -sh /path/to

## 2/14/15

setting up new ec2 instance for development, quick checklist

1. launch instance (Amazon linux)
1. ssh `ec2-user`
1. create `scott` user (see above)
1. scp `authorized_keys` file to `/home/scott/.ssh/`
1. add `scott` to `/etc/sudoers.d/` somewhere

        echo "scott ALL=(ALL) ALL" >> /etc/sudoers.d/00_foo

1. ssh `scott`
1. `yum install tmux git`
1. generate new key for github
1. git clone stuff (dotfiles, website)
1. build emacs from src (see above or `emacs.md`)
    a. `yum install gcc autoconf automake texinfo ncurses-devel
    pkgconfig`
1. apache2 `yum install httpd mod_ssl`
1. `yum install links`
1. make user dir readable, executable `chmod`
1. mod_php
1. mysql

## 3/09/15

    pgrep -fl foo

## 3/16/15

emacs tramp mode: using su to edit stuff as root

    C-x C-f /su::/etc/hosts RET

get fingerprint of httpd cert (see `ssl.conf`)

    sudo openssl x509 -fingerprint -in foo.crt

or

    sudo openssl x509 -fingerprint -in foo.crt -sha256

## 4/6/15

deleting a git tag locally and remotely

    git tag -d footag
    git push --delete origin footag

## 4/9/15

make an existing git branch track a remote branch

    git branch -u origin/foo
    git branch -u origin/foo foo
    git branch --set-upstream-to origin/foo

## 4/10/15

tmux - search pane in copy mode (similar to emacs)

Search down

    Ctrl-s
    [phrase]
    Enter
    n

Search up

    Ctrl-r

## 4/13/15

copy-paste in tmux: in copy mode select with `ctrl-space`, copy with
`ctrl-w`, paste with `M-]`

emacs replace-string with newline

    C-q C-j return

work vm quickstart - RHEL

    yum install screen tree emacs-nox

(currently version 23.1 of emacs - boo!)

    echo "escape ^]]" > .screenrc
    put key in ~/.ssh/ 
    
## 4/18/15
    
ec2 instance updates - wrong httpd package

http://serverfault.com/questions/570821/amazon-linux-lamp-with-php-5-5

    repoquery --requires php55
    yum list installed http*
    sudo yum remove httpd.x86_64 httpd-tools-2.2.29-1.4.amzn1.x86_64
    sudo yum install php55 httpd24 
    
## 5/7/15

Git - find first instance of token STATIC_PATH in commit history:

    git log -S STATIC_PATH --source --all

## 5/17/15

Emacs line-wrapping and fill column: see `fill-column` variable

    M-q
    M-x fill-paragraph
    C-x f
    M-x set-fill-column
    (setq-default fill-column 80)
    M-x column-number-mode

## 5/24/15

more on kirkwoodcoc ec2 instance...

install: `php55`, `httpd24`, `mod24_ssl`, `mysql55`, `mysql55-server`, `php55-mysqlnd`

    sudo service mysqld start|status|stop


output from starting:
{quote}
PLEASE REMEMBER TO SET A PASSWORD FOR THE MySQL root USER !
To do so, start the server, then issue the following commands:

/usr/bin/mysqladmin -u root password 'new-password'
/usr/bin/mysqladmin -u root -h ip-172-30-0-142 password 'new-password'

Alternatively you can run:
/usr/bin/mysql_secure_installation

You can start the MySQL daemon with:
cd /usr ; /usr/bin/mysqld_safe &

You can test the MySQL daemon with mysql-test-run.pl
cd /usr/mysql-test ; perl mysql-test-run.pl
{quote}

# install php mysql extension

"Your PHP installation appears to be missing the MySQL extension which is required by WordPress."

Find extensions dir:

    sudo php -i | grep extension

found

    extension_dir => /usr/lib64/php/5.5/modules => /usr/lib64/php/5.5/modules

install `php55-mysqlnd`

apache logs: `/var/log/httpd/`

## 5/25/15

Back to php 5.3, httpd 2.2

    sudo yum remove httpd24 mod24_ssl php55-mysqlnd
    sudo yum install httpd httpd-tools-2.2.29-1.4 mod_ssl php php-mysqlnd

## 5/29/15

git clone dotfiles into my existing home dir (may have to move files out of way)

    git init
    git remote add origin git@blahblahblah
    git fetch origin
    git checkout -b ubuntu-server --track origin/ubuntu-server

a good sequence to migrate to a new jumpbox virtual machine vm

* setup ssh
* `sudo apt-get install git emacs24-nox tmux zile tree openjdk-7-jdk`
* git clone dotfiles (see above)
* exit, relaunch tmux
* git clone dev project(s)
* lein self install

maven2 wasn't needed
openjdk-8 isn't available via ubuntu yet w/o ppa


## 5/30/19

more on kirkwoodcoc on ec2...

* done migrating back to Apache 2.2, php 3
* permalinks broken (404), had to change `AllowOverride None` to `AllowOverride All` in

        /etc/httpd/conf/httpd.conf

  Under `Directory` for kirkwoodcoc

## 6/4/15

lein-dist

* lein-package plugin (user pliant on GitHub)
* lein-dist teradata plugin, defines `dist`, `rpm` tasks
* add hooks to project.clj, e.g.:

        :hooks [leiningen.package.hooks.deploy leiningen.package.hooks.install]

* define `:package` and `:dist` values in project.clj
* invoke via hooked e.g. `install` or manually e.g.

        lein package
        lein dist
        lein rpm
 
## 6/17/15

mount the Linux-mountable share on a cloud VM:

    sudo mount thehost:/vol/path/to /mnt/blah2
    sudo umount /mnt/blah2

## 7/1/15

git export commit patch

    git format-patch

apply patch

    git am

## 7/6/15

TEZ troubleshoot log checklist

* loom-server.log

* hive.log

        /tmp/app.user.name/hive.log
        ${java.io.tmpdir}/${user.name}

* JobHistory logs

        MapReduce2 service, History Server component
        tdh125m2
        /var/opt/teradata/log/hadoop-mapreduce/mapred/

* ResourceManager and find the logs

        YARN service, Resource Manager component
        tdh125m1 (active)
        /var/opt/teradata/log/hadoop-yarn/yarn/
        ${yarn.nodemanager.log-dirs}
        
## 7/8/15

docker

    docker build -f tempfile -t nugent
    docker build -f tempfile -t nugent .
    docker run -t -i nugent /bin/bash
    docker run -t -i nugent sudo -H -u docker /bin/bash
 
## 7/10/15

problem with certs in curl, ubuntu 14:

    curl: (60) error setting certificate verify locations:
      CAfile: /usr/share/centrifydc/apache/certs/ca-certs.crt
      CApath: none

    More details here: http://curl.haxx.se/docs/sslcerts.html

try
    curl -V

temp workaround
    export CURL_CA_BUNDLE=/etc/ssl/certs/ca-certificates.crt

location of certs:
    /etc/ssl/certs/

Centrify OpenSSH replaces stock OpenSSH impl
    dpkg -l | grep centrify

yields matches on new jumpbox, none on old.

    $ locate sshd_config
    /etc/centrifydc/ssh/sshd_config
    /etc/ssh/sshd_config

* centrifydc - Centrify DirectControl infrastructure
* adclient - centrify Active Directory support

http://community.centrify.com/t5/DirectControl-Express-for-UNIX/Curl-OpenSSL-certificate-question/td-p/15539

`ldd` - print shared library dependencies e.g.

    ldd /usr/sbin/sshd | grep -i gssapi

startup services

    update-rc.d FOO defaults
    update-rc.d -f FOO defaults

    service --status-all

## 7/14/15

clone single branch of large project

    git clone --single-branch --branch release-0.5.2 git@github.com:apache/tez.git

java thread dump

    kill -3 jvm-pid

## 7/16/15

epiphany about the purpose of shims: code may be compiled (javac) using
completely different .jars|artifacts than are available at runtime (java);
java classpath may be built dynamically, finding provided jars of differing
versions. (Hadoop, Android, etc.)

## 7/17/15

running hive unit tests on the build box

* ssh to build slave
* switch to jenkins (assuming I'm a sudoer): `sudo su jenkins`
* `cd /var/lib/jenkins/workspace/temp-loom/` (git clone if necessary)
* `export WORKSPACE=/var/lib/jenkins/workspace/temp-loom`
* `./build-plugins`
* `lein copylib`  (accomplishes same thing as `lein test :jenkins`)
* `./prebuilt-hive-tests.sh`

applying a patch
    git am patchfile.patch

deleting a remote branch after merge
    git push origin --delete foobranch
    git push origin :foobranch

## 7/23/15

hive shell

    /usr/hdp/current/hive-client/bin/hive -f hql.txt

hive warehouse, HDP

    hadoop fs -ls /apps/hive/warehouse/

Cloudera (CDH)

    hadoop fs -ls /user/hive/warehouse

## 7/28/15

    docker save --output=proto-jenkins-temp.tar proto-jenkins-temp:latest
    docker load --input /tmp/proto-jenkins-temp.tar

    docker run --entrypoint="" -t -i -v $WORKSPACE:/home/docker/workspace proto-jenkins-lein

## 7/30/15

ssh-agent revisited

    ssh-agent -s > foo
    source foo

Now other terminals can `source foo` for the same env vars.

## 7/31/15

docker, enter running container interactively

    docker exec -it [container-id] bash

rename image

    docker tag [currentname]:latest [newname]:latest

remove image tag (leaving image intact)

    docker rmi [tag]

## 8/5/15

putty - ssh to virtualbox vm via port forwarding.

* In vm,
        sudo apt-get install openssh-server
* In vm manager, settings->network, port forwarding button, add rule:
  ssh, TCP, host port 3022, guest port 22
* In putty, connect to 127.0.0.1 port 3022
  under connection->ssh->tunnels, add a new rule:
  source port: 3022
  destination: 127.0.0.1:22

## 8/6/15

tmux, pop split pane out of window into its own window; join back to original
window (window #2 in this example)

    :break-pane
    :join-pane -t 2

git, change remote url

    git remote set-url origin git@github.com:revelytix/rsc-ls.git

## 8/10/15

    netstat -pan | grep 10000

## 8/17/15

extract RPM contents w/o installing RPM

    rpm2cpio foo.rpm | cpio -idmv

where `cpio` args are:
-i = extract
-d = make directories
-m = preserve modification time
-v = verbose

## 8/25/15

start virtualbox vm headless on Windows

    "C:\Program Files\Oracle\VirtualBox\VBoxManage.exe" startvm dev --type headless

also

    list vms
    controlvm dev poweroff

Quick Docker install - Ubuntu
http://docs.docker.io/en/latest/installation/ubuntulinux/

    sudo sh -c "echo deb http://get.docker.io/ubuntu docker main\
    > /etc/apt/sources.list.d/docker.list"

    sudo apt-get install lxc-docker

## 8/26/15

centrify authentication flush cache after changing password

    sudo adflush

docker-related networking

    apt-get install iputils-ping

* `resolveconf`
* `dnsmasq`
* Ubuntu's NetworkManager

tmux change status bar color

    set -g status-bg black
    set -g status-fg white

## 8/27/15

on edge node, creating hbase table & corresponding hive external table

https://github.com/romainr/hadoop-tutorials-examples/tree/master/hbase-tables

1. Generate column names and data with create_schemas.py. Run it with ./create_schemas.py
2. Upload the date data /tmp/hbase-analytics.tsv to HDFS with File Browser (same path)
3. In HBase Browser create  table with
4. Load the data into the analytics table with the HBase bulk import command.total3 , daycolumn , hourfamilies analyticsa 

Useful commands

    hbase shell
    $ list
    $ help cmd
    $ create "mytable", "columnfamily1", ...
    $ describe "mytable"
    $ scan "mytable"
    $ scan "mytable", {COLUMNS => "columnfamily1:"}
    $ scan "mytable", {COLUMNS => "columnfamily1:columnname"}
    $ version

    hive --version
    hive
    $ use databasename;
    $ show create table mytablename;
    $ CREATE EXTERNAL TABLE analytics_total_us (key int, tot string)
    ROW FORMAT SERDE 'org.apache.hadoop.hive.hbase.HBaseSerDe'
    STORED BY 'org.apache.hadoop.hive.hbase.HBaseStorageHandler'
    WITH SERDEPROPERTIES ("hbase.columns.mapping" = ":key,total:US")
    TBLPROPERTIES("hbase.table.name" = "analytics");

Debugging empty Hive external table (populated table in HBase)

Jim recommends checking logs of: hive; metastore; resource manager or job
history (if Hive submits a MR or Tez job)

In Ambari
* MapReduce2 QuickLinks contain JobHistory
* YARN QuickLinks contain ResourceManager

on tdh146m1:

    tdh146m1:~ # locate tdh146m1.log
    /var/opt/teradata/log/ambari-metrics-collector/hbase-ams-master-tdh146m1.log
    /var/opt/teradata/log/hadoop-yarn/yarn/yarn-yarn-resourcemanager-tdh146m1.log
    /var/opt/teradata/log/hadoop-yarn/yarn/yarn-yarn-timelineserver-tdh146m1.log
    /var/opt/teradata/log/hadoop/hdfs/hadoop-hdfs-journalnode-tdh146m1.log
    /var/opt/teradata/log/hadoop/hdfs/hadoop-hdfs-namenode-tdh146m1.log
    /var/opt/teradata/log/hadoop/hdfs/hadoop-hdfs-zkfc-tdh146m1.log
    /var/opt/teradata/log/hbase/hbase-hbase-master-tdh146m1.log

on tdh146m2:

    tdh146m2:~ # locate tdh146m2.log
    /var/opt/teradata/log/hadoop-mapreduce/mapred/mapred-mapred-historyserver-tdh146m2.log
    /var/opt/teradata/log/hadoop-yarn/yarn/yarn-yarn-resourcemanager-tdh146m2.log
    /var/opt/teradata/log/hadoop/hdfs/hadoop-hdfs-journalnode-tdh146m2.log
    /var/opt/teradata/log/hadoop/hdfs/hadoop-hdfs-namenode-tdh146m2.log
    /var/opt/teradata/log/hadoop/hdfs/hadoop-hdfs-namenode-tdh146m2.log.1
    /var/opt/teradata/log/hadoop/hdfs/hadoop-hdfs-zkfc-tdh146m2.log
    /var/opt/teradata/log/hbase/hbase-hbase-master-tdh146m2.log

also

    /tmp/[username]/hive.log
    /var/opt/teradata/log/hive/hivemetastore.log

(The verdict: user error, duh. Bad external table column mapping.)

## 8/28/15

manual logrotate

    logrotate --force /etc/logrotate.d/loom

## 8/31/15

curl foo to capture and use a session cookie in bash script (simple authentication)

    read -p "username: " ACCOUNT
    read -s -p "pwd: " PASSWORD

    export SESSION=$(curl -s -i -X POST -d "{\"username\":\"${ACCOUNT}\",\"password\":\"${PASSWORD}\"}" \
        -H "Content-type: application/json" http://${HOST}:${PORT}/api/path/to/login \
        | grep -i Set-Cookie | cut -f1 -d\; | cut -f2 -d=)

    curl --cookie session-id=$SESSION -H "Content-type: application/json" ...

## 9/2/15

    curl --manual | less

## 9/3/15

commit, name and tag a new image from a container:

    docker commit <Container ID> <Name>:<Tag>

## 9/10/15

emacs search, toggle case-sensitivity: `M-c`

new group, add to `hdfs` group

    groupadd foo
    useradd -g foo -G hdfs foo

## 9/11/15

sent an e-mail from within emacs, `M-x mail` mode! Via smtp server.

## 9/14/15

temp lein test selector

    :test-selectors { ...
    :foo (fn [m] (and (.startsWith (str (:ns m)) "some.test.namespace") (:test-selector m)))

## 9/18/15

list open files: `lsof`

    lsof -i :<port>

set of file descriptors open in a process
    ls -l /proc/<pid>/fd

## 9/21/15

add user to sudoers in SLES

    visudo

(edits `/etc/sudoers` file)

## 9/25/15

Python HTTP server from current working directory

    python -m SimpleHTTPServer [port]

Windows `hosts` file:

    systemroot\System32\Drivers\Etc\hosts

## 9/29/15

`chkconfig` stuff

    chkconfig --del loom

    chkconfig --level 345 loom on

    chkconfig --list loom
    loom            0:off   1:off   2:off   3:on    4:on    5:on    6:off

    find /etc/rc.d/ | grep loom

## 9/30/15

install pip using python easy_install; aws cli using pip

    python --version
    sudo easy_install pip
    sudo pip install awscli

upload to s3 bucket

    aws configure
    aws s3 ls
    aws s3 ls s3://bucket-name/path/to/

VirtualBoxHeadless configure, open a `.ova` image

    apt-get install virtualbox, virtualbox-dkms
    VBoxManage import foo.ovf
    VBoxManage list vms

set up port-forwarding rule:

    VBoxManage modifyvm "foo-vm" --natpf1 "ssh,tcp,127.0.0.1,2222,,22"

deactivate hardware virtualization acceleration

    VBoxManage modifyvm "foo-vm" --hwvirtex off

Set password for VNC connection. (If Oracle's proprietary extension pack isn't
installed, then we are limited to VNC connection. Otherwise the better `VRDE`
protocol is enabled. Windows can connect via native `mstsc` client.)

    vboxmanage modifyvm "foo-vm" --vrdeproperty VNCPassword=nuuuge

    VBoxManage showvminfo "foo-vm"
    VBoxManage controlvm "foo-vm" poweroff

flag `--vrde` controls vrde|vnc server

    VBoxHeadless -startvm "foo-vm" --vrde off

D'oh: https://www.virtualbox.org/manual/ch03.html#intro-64bitguests

## 10/6/15

aws s3 cli

see ACL for bucket

    aws s3api get-object-acl --bucket foo-bucket --key path/to/
    aws s3api get-object-acl --bucket foo-bucket --key path/to/filename

set ACL, grant permissions

    aws s3api set-object-acl --bucket foo-bucket --key path/to/filename --grant-read 'uri="http://acs.amazonaws.com/groups/global/AllUsers",uri="http://acs.amazonaws.com/groups/global/AuthenticatedUsers"' --grant-full-control 'id="longhexuuid"'
    
## 10/15/15-21

### Leiningen upgrade

* Currently on `2.0.0`
* want `2.5.1` (latest still using Clojure 1.6)
* `2.4.3` works w/o mods
* plugin `[lein-pprint "1.1.1"]`
* `2.0.0` -> `2.4.3`
  * lein included version of cemerick's `pomegranate` goes from `0.0.13` to `0.3.0`
  * upgrade `lein-package` from `2.0.1` to `2.1.0`
* `DEBUG=y lein foo` prints lein debug output
* run leiningen locally
  * `cd [project]/leiningen-core`
  * `lein bootstrap`
  * then invoke `[project]/bin/lein`

questions
* reduce compilations
  * `lein-package` plugin - reuse compilations?
  * `project.clj` - change `:prep-tasks` ?

inside docker container, hadoop pseudo-cluster, found logs at:

    tar czvf hadoop-logs.tar.gz /var/log/hadoop-hdfs /var/log/mysql /var/log/hive /var/log/hadoop-0.20-mapreduce ...

## 10/29/15

update node PPA

    sudo apt-add-repository -r ppa:chris-lea/node.js
    curl --silent --location https://deb.nodesource.com/setup_4.x | sudo bash -
    sudo apt-get install --yes nodejs

## 11/2/15

Node

    node -v
    v0.12.7
    npm -v
    2.11.3

    sudo apt-get install g++

    # Uninstall everything, start from clean slate
    sudo apt-add-repository -r https://deb.nodesource.com/node_4.x/trusty/main
    sudo rm /etc/apt/sources.list.d/nodesource.list*
    rm -fr node_modules/
    rm -fr ~/.npm
    sudo apt-get remove -y nodejs
    sudo apt-get autoremove
    sudo apt-get clean
    sudo apt-get update
    sudo rm -fr /usr/lib/node_modules

    # Install node 0.12, npm 2.11.3
    curl -sL https://deb.nodesource.com/setup_0.12 | sudo -E bash -
    sudo apt-get install -y nodejs

    # Install gulp globally
    sudo npm install -g gulp

    # And finally...
    npm install

## 11/3/15

Have `.profile` create, or reuse, `~/.sshagent` file

Clean git working directory of untracked files

    git clean -d -x --force --quiet

## 11/5/15

emacs regex with whitespace

    \s-stringtomatch

## 11/10/15

    M-x vc-git-grep

## 11/11/15

bash one-liner to see npm package name, version for all packages in `node_modules` directory

    for mo in `ls node_modules`; do cat "node_modules/$mo/package.json" | python -c 'import sys, json; packg=json.load(sys.stdin); print packg["name"], packg["version"]'; done

    diff -r <dir1> <dir2>

## 11/16/15

    ~/dev$ diff -r ui/node_modules/gulp-minify-css/ ui2/node_modules/gulp-minify-css/ | less

## 11/17/15

sigterm, from `signal.h`, for `kill` command
* 1 is `SIGHUP`, terminal hangup
* 2 is `SIGINT`, interrupt, equivalent to Ctrl-c
* 3 is `SIGQUIT` (use to get Java thread dump)
* 9 is `SIGKILL`
* 15 is `SIGTERM`, the default

## 11/30/15

dired, omit `node_modules`

hashsum on unix, windows

* unix

        shasum -a 256  path/to/file

* windows

        CertUtil -hashfile /path/to/file SHA256

## 12/17/15

zipping and tar'ring

    tar czvf foo.tar.gz dir1/ dir2/
    tar xvf foo.tar.gz
    tar tf foo.tar.gz
    zip -r foo.zip dir1/
    unzip foo.zip
    unzip -l foo.zip

## 1/23/16

install Java 8; update java alternative to JDK 1.8 on amazon linux ec2 instance

    yum search java
    sudo yum install java-1.8.0-openjdk-headless.x86_64
    ll /usr/lib/jvm/
    alternatives --usage | less
    alternatives --display java
    sudo alternatives --set java /usr/lib/jvm/jre-1.8.0-openjdk.x86_64/bin/java
    java -version
    
Mac OS Yosemite hosts file: `/private/etc/hosts`

## 2/2/16

First two days at DataStax

# Setting up MacBook Pro

* had to install XCode to get git (should have just installed XCode-cli but oh well)
* new ssh key, add to GitHub keys, git clone stuff
* onboarding script using Ansible Playbook (running into Ansible bugs)

        https://github.com/ansible/ansible/issues/13728

* Ansible installed HomeBrew
* I used brew to install emacs

        brew install emacs --with-cocoa
        brew linkapps emacs

* on emacs startup, initially got a compilation error - technomancy starter kit dependency on dash 2.12.1 (had to install that version by hand using `M-x package-list-packages`)
* Lots of hand-tweaking of dotfiles

## 2/3/16

# Day 3 - Wed

* CCM `2.1.3` installed via `pip`
* 3-node DSE 4.8.0 cluster

        ccm create dse-480-1 --dse --dse-username=your_username --dse-password=your_password -v 4.8.0 -n 3

where uname/password is from download site

# OS X keybindings

Struggling to find balance between command key and tmux|terminal Meta-keybindings I'm used to

Got it!
* Leave stock global keybindings alone
* in iTerm preferences
  * Keys: Change right command key to `option`
  * Keys: `+`, then add `cmd-`whatever combos to ignore
  * Profiles->Keys: Option should send `+Esc`

Almost all the cmd keybindings I care about (cmd-w, cmd-q, cmd-c, cmd-v, cmd-x, cmd-tab) happen to be left command key chords. Likewise, almost all the tmux and terminal meta-key combos I care about happen to be right meta key chords (M-d, M-f, M-v). Notable exceptions: M-<, M->.

## 2/4/16 - Thu

telnet host port - all-purpose check for any process listening on a port?
learn: nmap, netcat

## 2/5/16

Paste into|from OS X Gnu Emacs from|to clipboard

    M-x clipboard-yank
    M-x clipboard-kill-region

See also http://www.emacswiki.org/emacs/CopyAndPaste

## Installing python deps

Trying to `pip install python-ldap`, Missing `sasl.h` file; had to do this:

    xcrun --show-sdk-path
    sudo ln -s <the_path_from_above_command>/usr/include /usr/include

...but looks like a better way would be

    pip install python-ldap \
      --global-option=build_ext \
      --global-option="-I$(xcrun --show-sdk-path)/usr/include/sasl"

Trying to `pip install -I pyOpenSSL=0.13`, got compilation error

    OpenSSL/crypto/crl.c:6:23: error: static declaration of 'X509_REVOKED_dup' follows non-static declaration

solution is to install `0.14`

    sudo pip install -r requirements.txt

    LDFLAGS:  -L/usr/local/opt/openssl/lib
    CPPFLAGS: -I/usr/local/opt/openssl/include

you should be putting those flags somewhere in `setup.py` IIRC

## 2/8/16

Generally, switching branches should be accompanied by invoking `ant`

alternatively
    npm prune, install, update

http://localhost:8888/opscenter/js/bower_components/util/doh/runner.html?testModule=ripcord.tests.all&boot=../../../ripcord-compiled/tests/dojoconfig.js,../../dojo/dojo.js
http://localhost:8888/opscenter/js/bower_components/util/doh/runner.html?testModule=ripcord.tests.unit.widgets.backups.snapshotspager&boot=../../../ripcord-compiled/tests/dojoconfig.js,../../dojo/dojo.js

emoticons: tumbleweed, waiting, upvote|downvote, disapproval, thisisfine, oldschool, cerealspit, derp, giggity, wat, lol, lolwut, paddlin, shrug, awyeah, iseewhatyoudidthere, success, tableflip, indeed (monocle), whynotboth, puke (rainbow), pokerface, badpokerface, salute

## 2/10/16

EC2, GCE, Azure

# python issue workaround

Use homebrew to install a (keg only) version of `openssl` that `pyOpenSSL` 0.13 will compile with:
    brew install homebrew/versions/openssl101

Install `pyOpenSSL`, compiling against this version of `openssl`
    LDFLAGS=-L/usr/local/opt/openssl101/lib CPPFLAGS=-I/usr/local/opt/openssl101/include pip install -I pyOpenSSL==0.13

## 2/11/16

UI build/config:

* ant `build.xml`          - `ant ui` runs `npm install`, gulp
* node npm `package.json`  => bower, gulp
* Gulp `Gulpfile.js`       - runs bower build for dependencies; sass; babel; tests; ...
* Bower `bower.json`       => dojo
* DOJO `build.profile.js`

Show all ignored and untracked files

    git ls-files --ignored --others --exclude-standard --directory

run python http server from `ripcord/opscenterd/src/js`, load http://localhost:8888/bower_components/util/doh/runner.html?testModule=...
or is it...?
http://localhost:8888/opscenter/js/ripcord/tests/bootstrap.html#ripcord/tests/foo/bar

## 2/13/16

cljs

in `hello world` terminal:

    java -cp cljs.jar:src clojure.main repl.clj

in `cljs` src terminal:

    ./script/build
    lein repl :headless :port 2112

install `mvn` on Amazon Linux

    sudo wget http://repos.fedorapeople.org/repos/dchen/apache-maven/epel-apache-maven.repo \
        -O /etc/yum.repos.d/epel-apache-maven.repo
    sudo sed -i s/\$releasever/6/g /etc/yum.repos.d/epel-apache-maven.repo
    sudo yum update
    yum search apache-maven
    yum info apache-maven
    sudo yum install -y apache-maven
    mvn --version

## 2/17/16

    sudo ifconfig lo0 alias 127.0.0.x up

## 2/23/16

ui, when switching between branches

    npm prune && npm install && npm update

and/or

    rm -fr ./node_modules
    npm cache clean && npm install

## 2/25/16

python pretty print JSON awesomeness

    cat some.json | python -m json.tool

anvil (alternative to python simple http server)

## 2/26/16

homebrew routine

    brew update
    brew outdated
    brew upgrade [foo]

also

    brew doctor
    brew --cache

## 2/29/16

JS typechecking:
* FaceBook `Flow`
* `Term` (sp?) - typechecking against JSDoc

## 3/3/16

Today's coolness:

* wrote a python script to examine an array of JSON returned from a RESTful API endpoint
* figured out how to send multiple params in a cURL cmd (was missing quotes, therefore shell was backgrounding the process because of the ampersand)

        curl -sS 'http://whatever:8888/blahblah?foo=bar&goo=gar' | ./awesome-python-script.py

* figured out how to map over a list in python
* in JS, using dojo, did some map, reduce
* debugged a unit test in Chrome, with breakpoints - figured out how to look for loading sources

## 3/3/16

using opsc from src, cluster is at `local/clusters/Test_Cluster.conf`

## 3/8/16

create solr core w/ ccm

http://docs.datastax.com/en/latest-dse/datastax_enterprise/srch/srchCreatCore.html

    ccm node1 dsetool create_core "OpsCenter".backup_reports generateResources=true

## 3/9/16

mac os x | BSD `locate` and `updatedb`

    man locate
    /usr/libexec/locate.updatedb

alternatively,

    brew install findutils

to get gnu `locate` and `updatedb`

## 3/10/16

prop|config files
* cassandra.yaml
* cassandra-rackdc.properties

opsc ports: 7100, 9042

keyspace = collection of tables
* replication factor, set per DC

replication factor (RF; writes; fixed); contrast w/ consistency level (CL; reads and writes; changes)
* SimpleStrategy - single DC
* NetworkTopologyStrategy - mult DC's

token range

single token node (node maps to final token in its range); contrast w/ vnodes (num_tokens in cassandra.yaml)

partitioner - hashes tokens from designated values in rows being added
* partition key: piece of primary key

hinted handoff - recovery for writes targeting offline node
* stored in `system.hints` keyspace

consistency level (CL)
* writes - how many nodes must respond write was made durable
* reads - how many nodes must respond with latest copy of data
* quorum aka majority = RF / 2 + 1
* immediate consistency aka ALL - highest latency

ccm [node] dsetool [cmd]
ccm [node] status - nodetool status
ccm [node] cqlsh
ccm [node] nodetool ring
ccm [node] nodetool getendpoints [keyspace] [table] [partition key value(s)]

write path
* Memtables - in-memory CQL tables, indexes
* CommitLog - append-only
* SSTables aka "Sorted String Tables" - Memtable snapshots flushed to disk, clearing heap - never changed, supercedes previous
* Compaction - periodic, of SSTables

bin/sstable2json

## 3/11/16

simple keyspace

    cqlsh> create keyspace foobar WITH replication = {'class': 'SimpleStrategy','replication_factor':2};
    cqlsh> use foobar;
    cqlsh:foobar> create table peeps (id int primary key, name text, address text, phone text);
    cqlsh:foobar> insert into peeps (id, name, address, phone) values ( 1, 'Scott', 'MO', '867-5309');
    cqlsh:foobar> select * from peeps;

     id | address | name  | phone
    ----+---------+-------+----------
      1 |      MO | Scott | 867-5309

    (1 rows)
    cqlsh:foobar> select token(id) from peeps;

     token(id)
    ----------------------
     -4069959284402364209

    (1 rows)
    cqlsh:foobar> consistency;
    Current consistency level is ONE.
    cqlsh:foobar> update peeps set phone='555-867-5309' where id=1;
    cqlsh:foobar> select * from peeps;

     id | address | name  | phone
    ----+---------+-------+--------------
      1 |      MO | Scott | 555-867-5309

    (1 rows)
    cqlsh:foobar>

and

    ccm node1 nodetool getendpoints foobar peeps 1;

## 3/14/16

pip uninstall, install diff version

    sudo pip uninstall foo; sudo pip install foo==1.0.1

cache at

    ~/Library/Caches/

## 3/16/16

TIL `S->|<` is sufficient to page up|down in `less`. (Am used to emacs `S-M->|<` for that)

## 3/23/16

ccm-create DSE 5.0 nightly

    pushd ${TMPDIR:-/tmp/}; curl --insecure --location https://qa-automaton:3U8ib5na4mvAVY5y@downloads-qa.datastax.com/enterprise/dse-5.0.0-bin.tar.gz | tar xv; popd
    ccm create new-hotness --dse -n 3 --install-dir=${TMPDIR:-/tmp/}dse-5.0.0

lein, cider, nrepl...here we go again

leiningen
* version: `2.5.2`

cider-nrepl
* version: upgrading from `0.8.2` to `0.11.0`
* `0.11.0` requires clj `1.7+` and lein `2.5.2+`
* in ~/.lein/profiles.clj

cider
* version: upgrading from `0.8.2` to `0.11.0` (marmalade)
* an emacs mode, package-installed via melpa, marmalade or whatnot
* in ~/.emacs.d/

Getting this when I `M-x cider-connect`:

    ;; Connected to nREPL server running on port 2112 on host localhost - nrepl://localhost:2112
    ;; CIDER 0.11.0 (Bulgaria), nREPL 0.2.10
    ;; Clojure 1.7.0, Java 1.8.0_65
    ...
    WARNING: CIDER requires nREPL 0.2.12 (or newer) to work properly

this is a clue...

    ~/dev/ripcord/agent $ lein do clean, compile, repl :headless :port 2112
    Retrieving cider/cider-nrepl/0.11.0/cider-nrepl-0.11.0.pom from clojars
    Retrieving org/clojure/tools.nrepl/0.2.12/tools.nrepl-0.2.12.pom from central
    Retrieving org/clojure/tools.nrepl/0.2.12/tools.nrepl-0.2.12.jar from central
    Retrieving cider/cider-nrepl/0.11.0/cider-nrepl-0.11.0.jar from clojars
    nREPL server started on port 2112 on host 127.0.0.1 - nrepl://127.0.0.1:2112

the answer: https://github.com/technomancy/leiningen/issues/2072

## 3/24/16

`ns-unmap` a namespace's interned symbols

    (map (comp (partial ns-unmap *ns*) first) (ns-interns *ns*))

## 3/25/16

Cassper
Guard Weiner Dog

## 3/28/16

TIL alternative to

    git lg --stat [commit range]

which is

    git diff --name-only [commit range]

## 3/29/16

    cqlsh> describe keyspaces;

## 3/30/16

CCM error

    Error opening zip file or JAR manifest missing : /Users/scottbale/.ccm/new-hotness/node3/resources/cassandra/bin/../../../resources/cassandra/lib/jamm-0.3.0.jar

Solution

This is all from `~/.ccm/clustername/node1`:

    ln -s ~/.ccm/repository/4.8.0/lib lib
    ln -s ~/.ccm/repository/4.8.0/resources/cassandra/lib resources/cassandra/lib
    ln -s ~/.ccm/repository/4.8.0/resources/dse/lib resources/dse/lib
    ln -s ~/.ccm/repository/4.8.0/resources/hadoop/lib resources/hadoop/lib

## 4/1/16

    cqlsh:OpsCenter> select event_time, blobAsBigInt(timestampAsBlob(event_time)), type from backup_reports where week='201614' ;
    select backup_id, event_time, blobAsBigInt(timestampAsBlob(event_time)) from backup_reports where week='201613' and event_time = '2016-03-30 20:35:24.250+0000' ;

## 4/4/16

quick checklist to wipe opsc clean
1. remove logs
1. drop opsc keyspace
1. revert cluster conf

drop opsc keyspace, in CQLSH

    cqlsh> describe keyspaces;
    cqlsh> drop keyspace "OpsCenter";


## 4/7/16

Per Phil, check out `logging.py`

## 4/14/16

TIL not to trust `jps`

    ~/.ccm/dse-perf-work/node1/resources/cassandra/conf/cassandra-env.sh

comment out
    # http://www.evanjones.ca/jvm-mmap-pause.html
    JVM_OPTS="$JVM_OPTS -XX:+PerfDisableSharedMem"

https://issues.apache.org/jira/browse/CASSANDRA-9483

> The default JVM flag -XX:+PerfDisableSharedMem will cause the following tools JVM
> to stop working. jps, jstack, jinfo, jmc, jcmd as well as 3rd party tools like Jolokia.
> If you wish to use these tools you can comment this flag out in cassandra-env.{sh,ps1}

opsc on-server backup dir: `snapshots` directory below the c* data dir (`/var/lib/cassandra/data` by default)
* for my `ccm` cluster, they're in `~/.ccm/[cluster-name]/nodeN/data0/[long-ascii-id]/snapshots/`
* see also `backup_staging_dir` and `tmp_dir` properties of agent `agent/local/address.yaml`
* the above overriden by `runmultiple.py` in `agent/local/agentN.yaml`

## 4/18/16

### OPSC-8349 notes:
* commit log stomp channel: `/commitlog/status`
  * incoming: Agents.py, `routeIncoming`
  * outgoing: common.clj, `update-commitlog-status`

#### OPSCD
* logging via twisted
* stomp via `StompFactory` of morbid (located in `opscenterd/lib/py/morbid/`); referenced by `OrbitedService`
* Agents.py - only 1 code route that results in a call to `cleanupPIT` with a non
  * see `routeIncoming` for dispatching
  * see `processNodeDetail` for example of trace logging 
  * `processCommitLogStatus` has very little logging
    * lack of existing log statements indicates status must be `running`, destination `ON_SERVER`

How do you turn up twisted logging to trace?
* in master, via `logback.xml`
* in 5.2.x, via `local\opscenterd.conf`

## 4/21/16

To enable commitlog archiving on local ccm agents, had to symlink the `archive_commitlog.sh.template` file:

    ln -s agent/pkg/bin/archive_commitlog.sh.template agent/bin/

fswatch - detect changes to directory tree:

    brew install fswatch
    fswatch -xt -e ".*\.log" ${TMPDIR:-/tmp/}dse-5.0.0 ripcord/opscenterd/local/ ripcord/agent/local/ ripcord/agent/tmp1/ ripcord/agent/tmp2/ ripcord/agent/tmp3/ ripcord/agent/backups1/ ripcord/agent/backups2/ ripcord/agent/backups3/  ~/.ccm/borscht/ /tmp/ >> fswatch.log 2>&1

## 4/22/16

### More OPSC_8349 notes

sub-namespaces under src/opsagent/backups/, ordered roughly by dependency:

common*
entities, staging*
throttler
destinations
pit*, snapshots
coordinator, restore
cleanup

## 4/27/16

merge script:

    /bin/merge.py master foo-branch

## 4/28/16

curl cmds for opsc backups, job schedules, requests:

create scheduled backup
    curl -sSX POST 'http://localhost:8888/Test_Cluster/job-schedules' --data '{"first_run_date":"2016-04-27","first_run_time":"15:45:00","timezone":"GMT","interval":5,"interval_unit":"minutes","job_params":{"type":"backup","keyspaces":["foobar"],"cleanup_age":30,"cleanup_age_unit":"days","destinations":{}}}' 

    curl -sSX POST 'http://localhost:8888/Test_Cluster/backups/destinations'  --data '[]'

job schedule (or DELETE)
    curl -sS 'http://localhost:8888/Test_Cluster/job-schedules/172ce740-2319-4407-a81f-94087677836a'

status of request
    curl -sS 'http://localhost:8888/request/5ee7a158-cebe-4424-8b53-6a0e31152277/status' 

delete backup
    curl -sSX DELETE 'http://localhost:8888/Test_Cluster/backups?tag=opscenter_b320e60d-48a6-4221-a1ff-5cea088a04d2_2016-04-27-21-20-00-UTC&destination=OPSC_ON_SERVER&remove_destination=Delete%20Backup%20Data' 

backups, backup activity
    curl -sS 'http://localhost:8888/Test_Cluster/backups/$keyspace'
    curl -sS 'http://localhost:8888/Test_Cluster/backup-activity?count=$N'
    curl -sS 'http://localhost:8888/Test_Cluster/backup-activity/full_status?week=201618&event_time=1462462500&backup_id=opscenter_ddbd74f0-4152-4dbd-92e8-f7f76a7eb4b2_2016-05-05-15-35-00-UTC&type=backup&destination=OPSC_ON_SERVER' 

## 5/3/16

What gulp tasks are available?

    ~/dev/ripcord/opscenterd $ ./node_modules/.bin/gulp

## 5/6/16

Gulp test

    ~/dev/ripcord/opscenterd $ ./node_modules/.bin/gulp test --suite ripcord/tests/unit/widgets/foo/barwidget

KMIP = offsite key storage (in DSE context)

https://en.wikipedia.org/wiki/Key_Management_Interoperability_Protocol
https://docs.datastax.com/en/latest-opsc/opsc/configure/opscConfigKMIPalert.html

## 5/9/16

python unit tests logged at `opscenterd/tests/test_run.log`

## 5/10/16

Python repl, you can either do:
    $ python
to get a python repl or
    $ ./opscenterd/bin/jython
to start a jython repl

## 5/17/16

ctool, part of automaton,

* `~/.automaton.conf`
* git clone github.com/riptano/automaton
* `export PYTHONPATH="/Users/scottbale/dev/automaton":${PYTHONPATH}`
* `export PATH="$PATH:/Users/scottbale/dev/automaton/bin"`
* login to openstack to see provisioning - use ldap credentials

> technically ctool is the commandline interface to automaton...usually referred to synonymously

     pip install python-openstackclient

python `virtualenv` https://virtualenv.readthedocs.org/en/latest/

## 5/18/16

More on openstack:

ignore custom images, dev stuff from https://github.com/riptano/ripcord/tree/master/opscenterd/tests/automaton/tests#local-usage

ssh public key fingerprint

    ssh-keygen -lf /path/to/key.pub

cmds: `openstack server list`, `nova host-list`, `keystone user-list`

## 5/19/16

AFTs
* ec2 region is hardcoded in AFTs
* When running AFTs use caution in syntax:

        test_file.py:TestClass.test_case

LCM = LifeCycle Manager (code-named Spock)
DSE Multi-Instance (formerly known as dense nodes)


mental queue
* jabber (distributed consensus) vs jmx, stomp, etc. - can opscd leverage?
* drivers
* rollups

Andy Tolberg - driver team - JobCreator project

## 5/20/16

ec2 instances powered off overnight - timeout?
AFT rerun created new instances rather than starting up prev ones

Q2 goals: DSE - self replication, spark

JIRA comments

scp patches
* compile class

        ./bin/jython
        >>> import py_compile
        >>> py_compile.compile('./src/path/to/Foo.py', '/path/to/Foo$py.class');

* scp class to target

        ctool scp2 scottbale_opsc Foo\$py.class 0:/home/automaton/

* on target, copy to `/usr/share/opscenter/jython/Lib/site-packages/opscenterd`
* restart

        sudo service opscenterd restart

* opscd log

        sudo tail -f /var/log/opscenter/opscenterd.log

## 5/23/16

AFT: Found agent logs at `~/dse0_agent/agent/log/agent.log`


misc recent commands:

    ./run.sh test_dense_nodes.py:TestDenseNodesRestart
    tail -f ~/dev/ripcord/opscenterd/tests/automaton/tests/testrun.log
    ./bin/opscenter -f > log/opscd.log 2>&1
    for i in {1..5}; do curl 'http://ec2-54-153-0-232.us-west-1.compute.amazonaws.com:8888/scottbalez/diagnostics.tar.gz' > "diagnostics_B$i.tar.gz"; done
    ctool scp2 scottbalez 1:/home/automaton/dse1_agent/agent/log/agent.log ../agent11.log

Bret's VBox setup notes

* network
  * adapter 1 - attached to: NAT (I should use Bridge)
  * adapter 2 -
* dense node cluster network
  * adapter 1 - attached to: Internal Network (descriptive string)  
  * adapter 2 - ditto

see OPSC-7542 notes
* address.yaml attachments
build agent tarball, scp to nodes

add node scripts

     /etc/dse-[name]/serverconfig/

## 5/25/16

VirtualBox network mode options
* NAT - Network Address Translation

## 5/31/16

OWASP Webgoat project
* entity encoder API

XSS - server vulnerabilities
* soln: validating input, encoding output

5 common HTML contexts
* Element content: `<div>RepeatAfterMe</div>`
* Attribute value: `<div id="RepeatAfterMe">`
* JavaScript: `<script>var a = "RepeatAfterMe";`
* CSS: `<div style="RepeatAfterMe" />`
* URL Attribute value: `<a href="RepeatAfterMe">`

CSRF aka Sea-Surf - browser vulnerabilities
* soln: make requests unpredictable|hard to forge via secret token in conversational state

fixed flyspell 
* `brew install aspell --with-lang-en`
* tweak `init.el`
