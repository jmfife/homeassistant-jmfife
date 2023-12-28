To install Docker: https://docs.docker.com/engine/install/ubuntu/

Make sure the current user is in the docker user group so the `run`` command can be executed without sudo.

To initially set up the Home Assitant container and start it:

```
$ docker run -d --name homeassistant --privileged \
--restart=unless-stopped \
-e TZ=America/Los_Angeles \
-v /home/jmfife/projects/homeassistant-jmf/config:/config \
-v /run/dbus:/run/dbus:ro \
--network=host ghcr.io/home-assistant/home-assistant:stable
```

I have scripted this, so you can just type `./start`

After the image is configured, you can stop or restart the container easily with the `docker stop homeassistant` and `docker start homeassistant` commands. For example, after a reboot, type `docker start homeassistant` to bring it back up with all of the configuration and state data it had when it was last running.

To access Home Assistant in Browser, go to http://localhost:8123/

Note:  To add Home Assistant Community Store (HACS) add-ons are not natively available for containerized installations. To get HACS into the container, follow https://hacs.xyz/docs/setup/download/




