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
