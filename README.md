[linuxserverurl]: https://linuxserver.io
[forumurl]: https://forum.linuxserver.io
[ircurl]: https://www.linuxserver.io/irc/
[podcasturl]: https://www.linuxserver.io/podcast/

[![linuxserver.io](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/linuxserver_medium.png)][linuxserverurl]

The [LinuxServer.io][linuxserverurl] team brings you another container release featuring easy user mapping and community support. Find us for support at:
* [forum.linuxserver.io][forumurl]
* [IRC][ircurl] on freenode at `#linuxserver.io`
* [Podcast][podcasturl] covers everything to do with getting the most from your Linux Server plus a focus on all things Docker and containerisation!

# lsioarmhf/ombi
[![](https://images.microbadger.com/badges/image/lsioarmhf/ombi.svg)](http://microbadger.com/images/lsioarmhf/ombi "Get your own image badge on microbadger.com")[![Docker Pulls](https://img.shields.io/docker/pulls/lsioarmhf/ombi.svg)][hub][![Docker Stars](https://img.shields.io/docker/stars/lsioarmhf/ombi.svg)][hub][![Build Status](http://jenkins.linuxserver.io:8080/buildStatus/icon?job=Dockers/LinuxServer.io-armhf/lsioarmhf-ombi)](http://jenkins.linuxserver.io:8080/job/Dockers/job/LinuxServer.io-armhf/job/lsioarmhf-ombi/)
[hub]: https://hub.docker.com/r/lsioarmhf/ombi/

Want a Movie or TV Show on Plex? Use [Ombi!][ombiurl]

[![medusa](https://raw.githubusercontent.com/linuxserver/beta-templates/master/lsiodev/img/plexrequests-banner.png)][ombiurl]
[ombiurl]: http://ombi.io

## Usage

```
docker create \
  --name=ombi \
  -v <path to data>:/config \
  -e PGID=<gid> -e PUID=<uid>  \
  -e TZ=<timezone> \  
  -p 3579:3579 \
  lsioarmhf/ombi
```

## Parameters

`The parameters are split into two halves, separated by a colon, the left hand side representing the host and the right the container side. 
For example with a port -p external:internal - what this shows is the port mapping from internal to external of the container.
So -p 8080:80 would expose port 80 from inside the container to be accessible from the host's IP on port 8080
http://192.168.x.x:8080 would show you what's running INSIDE the container on port 80.`



* `-p 3579` - the port(s)
* `-v /config` - where ombi should store config files.
* `-e PGID` for GroupID - see below for explanation
* `-e PUID` for UserID - see below for explanation
* `-e TZ` for timezone information, eg Europe/London

It is based on alpine linux with s6 overlay, for shell access whilst the container is running do `docker exec -it ombi /bin/bash`.

### User / Group Identifiers

Sometimes when using data volumes (`-v` flags) permissions issues can arise between the host OS and the container. We avoid this issue by allowing you to specify the user `PUID` and group `PGID`. Ensure the data volume directory on the host is owned by the same user you specify and it will "just work" ™.

In this instance `PUID=1001` and `PGID=1001`. To find yours use `id user` as below:

```
  $ id <dockeruser>
    uid=1001(dockeruser) gid=1001(dockergroup) groups=1001(dockergroup)
```

## Setting up the application
`IMPORTANT... THIS IS THE ARMHF VERSION`

Webui is at `<your-ip>:3579`, sign in with your plex username. More info from [ombi][ombiurl]

## Info

* Shell access whilst the container is running: `docker exec -it ombi /bin/bash`
* To monitor the logs of the container in realtime: `docker logs -f ombi`

* container version number 

`docker inspect -f '{{ index .Config.Labels "build_version" }}' ombi`

* image version number

`docker inspect -f '{{ index .Config.Labels "build_version" }}' lsioarmhf/ombi`

## Versions

+ **14.01.17:** Initial Release Date.
