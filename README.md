<h1 align="center">LibreY</h1>

[![Docker Image CI](https://github.com/Ahwxorg/LibreY/actions/workflows/docker-image.yml/badge.svg)](https://github.com/Ahwxorg/LibreY/actions/workflows/docker-image.yml)

> LibreY is a fork of LibreX, a framework-less and javascript-free privacy respecting meta search engine, made by [hnhx](https://github.com/hnhx). LibreY changed some features like automatic redirection. The original code is written by [hnhx and contributors](https://github.com/hnhx/LibreX/contributors)

<p align="center">
  <img src="https://user-images.githubusercontent.com/49120638/215327189-76c54dec-8b19-4faf-8c39-29a61aa3b143.png" width="400">
  <img src="https://user-images.githubusercontent.com/49120638/215327239-b2a1cb07-3773-4ae7-bb3b-738de2cc3161.png" width="400">
</p>

<p align="center"></p>

<br>

## Matrix

If there's an important announcement, we do have a Matrix chatroom which you can join over at #librey:ahwx.org.

### Instances

You can find a list of instances on any LibreY instance by accessing /instances.php.<br>
Alternatively look at `instances.json` where the list is generated from.<br><br>
While the official instances may be more updated and have better uptime, please consider using another person's instances as these are heavily overloaded.<br>
Support the community. ❤️<br><br>
[@Ahwxorg](https://github.com/Ahwxorg)'s instance:<br>
[search.ahwx.org](https://search.ahwx.org/instances.php)<br>
[Tor](http://wn5jl6fxlzzfenlyu3lc4q7jpw2saplrywxvxtvqbguotwd4y5cjeuqd.onion/instances.php)<br>
[search2.ahwx.org](https://search2.ahwx.org/instances.php)<br>
[Tor](http://hyy7rcvknwb22v4nnoar635wntiwr4uwzhiuyimemyl4fz6k7tahj5id.onion/instances.php)<br>
[search3.ahwx.org](https://search3.ahwx.org/instances.php)<br>
[Tor](http://r7nesn6dnp2fssinw7n5uj4ob2na6g4jppakpjgioxb6v4ca4bbsqoyd.onion/instances.php)<br>
<br>
[@davidovski](https://github.com/davidovski)'s instance:<br>
[search.davidovski.xyz](https://search.davidovski.xyz/instances.php)<br>
<br>
[@codedipper](https://github.com/codedipper)'s instance:<br>
[librex.me](https://librex.me/instances.php)<br>
[librex.revvy.de](https://librex.revvy.de/instances.php)<br>
[Tor](http://librex.revvybrr6pvbx4n3j4475h4ghw4elqr4t5xo2vtd3gfpu2nrsnhh57id.onion/instances.php)<br>
[I2P](http://revekebotog64xrrammtsmjwtwlg3vqyzwdurzt2pu6botg4bejq.b32.i2p/instances.php)<br>
<br>

### How to host LibreY

To host LibreY using Docker, you can follow the instructions in the [Docker directory](https://github.com/Ahwxorg/LibreY/tree/main/docker).

To host LibreY using your OS's native package manager and PHP+NGINX, you can follow the following steps:

These instructions are for Debian GNU/Linux but it should be similar on all GNU/Linux distros (alter the `apt` commands and `systemctl` commands to suit your distros native package management and init service.) and \*BSD systems.

Install the packages

```sh
sudo apt install php php-fpm php-dom php-curl php-apcu nginx git
```

Clone LibreY

```sh
git clone https://github.com/Ahwxorg/LibreY.git
```

Rename the config and opensearch file

```sh
cd librey
mv config.php.example config.php
mv opensearch.xml.example opensearch.xml
```

Change opensearch.xml to point to your domain

```sh
sed -i 's/http:\/\/localhost:80/https:\/\/your.domain/g' opensearch.xml
```

Example nginx config

```sh
server {
        listen 80;

        server_name your.domain;

        root /var/www/html/LibreY;
        index index.php;

        location ~ \.php$ {
               include snippets/fastcgi-php.conf;
               fastcgi_pass unix:/run/php/php-fpm.sock;
        }
}
```

You could also remove the php extension, which is optional. Add this code inside the `server {}` block.

```sh
location / {
       try_files $uri $uri/ @extensionless-php;
}

location @extensionless-php {
       rewrite ^(.*)$ $1.php last;
}
```

Start php-fpm and nginx

```sh
sudo systemctl enable --now php-fpm nginx
```

Now LibreY should be running!

### About LibreY

LibreY gives you text results from Google, DuckDuckGo, Brave Search, Ecosia, Yandex Search and Mojeek. LibreY provides images from Qwant, and torrents from i.e. Ahmia and popular torrent sites. LibreY does this without spying on you.
<br>LibreY doesn't save **any** type of data about the user, there are no logs (except NGINX logs if the host sets them).

### LibreY compared to other metasearch engines

| Name    | Works without JS     | Privacy frontend redirect | Torrent results | API | No 3rd party libs used |
| ------- | -------------------- | ------------------------- | --------------- | --- | ---------------------- |
| LibreY  | ✅                   | ✅                        | ✅              | ✅  | ✅                     |
| SearXNG | ❓ Not user friendly | ❓ Only host can set it   | ✅              | ✅  | ❌                     |
| Whoogle | ✅                   | ❓ Only host can set it   | ❌              | ❌  | ❌                     |
