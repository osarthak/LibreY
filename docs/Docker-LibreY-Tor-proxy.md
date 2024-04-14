> [!IMPORTANT]  
> Please note that this heavily relies on [@codedipper](https://github.com/codedipper)'s [work and is basically a copy of his wiki](https://github.com/codedipper/LibreY-Tor).


Step 0: Install and configure Docker.
Step 1: Enter a root shell on the host machine.

Step 2: Clone the required git repositories to the host machine.

```sh
git clone https://github.com/Ahwxorg/LibreY.git LibreY/
git clone https://github.com/codedipper/LibreY-Tor.git LibreY-Tor/
```

Step 3: Apply the docker-compose.yml patch.

```sh
cd LibreY/
git apply ../LibreY-Tor/LibreY_docker-compose-yml.diff
```

Step 4: Manually edit `LibreY/docker-compose.yml` and `LibreY-Tor/torrc` to configure LibreY and Tor to your liking.

To update containers:

```sh
cd LibreY/
docker compose down
docker compose pull
docker compose up -d
```

It is recommended to build the images yourself to avoid an outdated Tor version.

TODO Documentation:

    Manually build images, `docker-compose`
    Manually build images, `docker run`
    Use prebuilt images, `docker run`
