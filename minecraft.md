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
