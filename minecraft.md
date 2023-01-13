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

## 5/24/21

minecraft 1.12.2 forge and mods
* stashed jar files in `/usr/local/minecraft/`

forge 1.12.2
* [universal installer](https://maven.minecraftforge.net/net/minecraftforge/forge/1.12.2-14.23.5.2855/forge-1.12.2-14.23.5.2855-installer.jar)

jar files (for server and client)
* [dragon mounts 2](https://media.forgecdn.net/files/2750/96/DragonMounts2-1.12.2-1.6.3.jar)
* [ancient warefare 2](https://media.forgecdn.net/files/3293/318/ancientwarfare-1.12.2-2.7.0.1038.jar)
  * "requires codechickenlib 3.2.3 or above"
  * [codechickenlib](https://media.forgecdn.net/files/2779/848/CodeChickenLib-1.12.2-3.2.3.358-universal.jar)
* [animania](https://media.forgecdn.net/files/3213/136/animania-1.12.2-base-2.0.3.28.jar)
  * "requires craftstudioapi any"
  * [craftstudioapi](https://media.forgecdn.net/files/2661/859/CraftStudioAPI-universal-1.0.1.95-mc1.12-alpha.jar)

TIL extended attributes
* https://superuser.com/questions/28384/what-should-i-do-about-com-apple-quarantine
* https://serverfault.com/questions/151997/what-does-the-symbol-mean-in-a-files-permission-settings

Client: notes from 8/23/14 still work, starting with `java -jar forge-...-installer.jar`
* launch ordinary minecraft, look for "forge" profile to launch game
* added `.jar` files to `mods/` dir

Server: Downloaded latest forge installer. Forgot to do the `--installServer` step which extracts the universal forge
jar from the installer forge jar _and_ downloads a bunch of libraries to `libraries/` (had a missing class before that)

Launching forge, first two tries caused OOM

## 5/25/21

how do you increase RAM?

    ~ $ grep "VM" /Applications/Minecraft.app/Contents/Info.plist
    ~ $ ls -la /Applications/Minecraft.app/Contents/Info.plist
    -rw-r--r--  1 corinne  admin  1261 May  8 16:49 /Applications/Minecraft.app/Contents/Info.plist
    ~ $ sudo chmod 666 /Applications/Minecraft.app/Contents/Info.plist
    Password:
    ~ $ ls -la /Applications/Minecraft.app/Contents/Info.plist
    -rw-rw-rw-  1 corinne  admin  1261 May  8 16:49 /Applications/Minecraft.app/Contents/Info.plist
    ~ $ sudo chmod 644 /Applications/Minecraft.app/Contents/Info.plist
    ~ $ ls -la /Applications/Minecraft.app/Contents/Info.plist
    -rw-r--r--  1 corinne  admin  1327 May 25 07:36 /Applications/Minecraft.app/Contents/Info.plist
