# Home Assistant and Music Assistant

To install Docker: https://docs.docker.com/engine/install/ubuntu/

Make sure the current user is in the docker user group so the `run`` command can be executed without sudo.

## Home Assistant

To initially set up the Home Assistant container and start it:

```
mkdir config
$ docker run -d --name homeassistant --privileged \
--restart=unless-stopped \
--network=host \
-e TZ=America/Los_Angeles \
-v /home/jmfife/projects/homeassistant-jmf/config:/config \
-v /run/dbus:/run/dbus:ro \
ghcr.io/home-assistant/home-assistant:stable
```

I have scripted this, so you can just type `./start`

After the image is configured, you can stop or restart the container easily with the `docker stop homeassistant` and `docker start homeassistant` commands. For example, after a reboot, type `docker start homeassistant` to bring it back up with all of the configuration and state data it had when it was last running.

To access Home Assistant in Browser, go to http://localhost:8123/

Note:  To add Home Assistant Community Store (HACS) add-ons are not natively available for containerized installations. To get HACS into the container, follow https://hacs.xyz/docs/setup/download/

## Music Assitant

The integration between Music Assistant and Home Assistant doesn't really work with a docker install.  Here is as far as I got...

To add music assistant, install the integration with HACS, then install and run a new docker container with:

```
mkdir media
docker run -d --name musicassistant \
--network host \
--privileged \
-v /home/jmfife/projects/homeassistant-jmfife/media:/data \
ghcr.io/music-assistant/server
```

This will serve a Music Assistant UI at http://localhost:8095

Again, after the image is configured, you can stop or restart the container easily with the `docker stop musicssistant` and `docker start musicssistant` commands. For example, after a reboot, type `docker start musicassistant` to bring it back up with all of the configuration and state data it had when it was last running.

I never could get the Music Assistant in the Home Assistant sidebar though...

