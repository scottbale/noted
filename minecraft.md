# My Minecraft Server
## v.1 - Nov '14 - simplest possible

Highlights

* Amazon EC2 t2.small instance (2 Gig RAM)
* Ubuntu 14 server 64 bit
* 8 Gig (default) EBS volume
* open port 25565 (Minecraft default) - custom TCP rule on security
  group
* install OpenJDK 7
* `wget` minecraft server 1.8 jar
* manually create accounts (one for me, one for minecraft server)
* scp bulpeppers files (tar'd, gzip'd)

Download server jar URL (example):

https://s3.amazonaws.com/Minecraft.Download/versions/1.9.4/minecraft_server.1.9.4.jar

## 8/23/14 minecraft mods

minecraft forge-src

    ./gradlew setupDecompWorkspace --refresh-dependencies

### server

install installer http://files.minecraftforge.net/ (remove `adfly` prefix
from URL)

    wget http://files.minecraftforge.net/maven/net/minecraftforge/forge/1.7.10-10.13.0.1208/forge-1.7.10-10.13.0.1208-installer.jar

run installer (headless)

    java -jar forge-1.7.10-10.13.0.1208-installer.jar --installServer

run universal jar (note manifest file defines a classpath, dependent
on libraries/ folder)

    java -jar forge-1.7.10-10.13.0.1208-universal.jar
    
### client, mac os x

for each logged in user:

First, user must play the version of Minecraft (1.7.10 in this
example) at least once prior to installing forge. This can be done by
creating an alternate profile, in which the (older) version of
Minecraft can be specified.

    java -jar forge-1.7.10-10.13.0.1208-installer.jar
    
starts GUI, prompts to install to

    /Users/[username]/Library/Application Support/minecraft
    
I stashed the MC forge universal installer on iMac at

    /usr/local/minecraft-forge/
    
### install a mod

http://minecraft.gamepedia.com/Mods/Installing_forge_mods

Shift-Cmd-G in `Finder` prompts for path

get mod `zip` file, install to

    /Users/[username]/Library/Application Support/minecraft/mods/

## 1/18/15

OS X - run Minecraft jar via command line

    java -d64 -jar /Applications/Minecraft.app/Contents/Resources/Java/Bootstrap.jar
    
Save to file called `something.command`, `chmod a+x` on it. (I stashed
it in `/Applications/`, then dragged onto the dock.)

## 11/5/17

bulpeppers status page: https://balehaus.org/bulpeppers.html
Bulpeppers minecraft version: 1.12.2
forge version: 1.12.2-14.23.0.2529

    wget http://files.minecraftforge.net/maven/net/minecraftforge/forge/1.12.2-14.23.0.2529/forge-1.12.2-14.23.0.2529-universal.jar

D upload his own world files from iMac to git:

    ~/Users/[username]/Library/Application Support/minecraft/saves/
    
    ssh-add [ssh key]
    git init
    git remote add -t master origin [aws codecommit url]

start server notes
* forge very nicely provides direct download links for installer jar and universal jar, plus
  checksums http://files.minecraftforge.net/
* D emailed me a bunch of links to mod jar downloads. Couldn't get them to download to server
  directly with `curl`. !@%!^#!^!! Had to download them all w/ browser, tar them up, and scp them to
  server.
* Put mod `.jar` files in `mods/` folder
* Forgot to install and run installer at first (see instructions above)
* startup logging gave me a bunch of warnings about version mismatches (from D creating the world
  files with different mod versions installed)

## 7/27/19

debugging clients
* `Unable to update the Minecraft Native Launcher`
* binary installed at `/usr/Applications/Minecraft.app`
* user local stuff installed at `~/Library/ApplicationSupport/minecraft/`
* Aha... `nativeUpdaterLog.txt` - permissions problem 
* decided to punt, installed copy for each user in their own `~/Applications/` folder, deleted shared copy at `/Applications/`

