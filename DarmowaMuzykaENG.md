# How to download music for free?

Probably many of you are nervous about Spotify because of adding unwanted playlists, the inability to view the source code of the application, which threatens your privacy and security, and finally the limited possibility to use music offline (you still need Spotify, which you have to run at least once every 30 days).

The solution to these problems may be for many people to use the `deezer` service, with which we will be able to download music files in MP3 and FLAC format and use them where we could not use Spotify - car radios etc.

1. Install the Docker - this will allow you to easily start the server without having to change the configuration of your computer (manual installing is also available).

In Ubuntu 20.04, you only need to run the command `apt install -y docker-compose docker.io`

For older versions of Ubuntu or Linux Mint, the following commands must be executed:
```
sudo apt update
sudo apt install -y apt-transport-https ca-certificates curl gnupg-agent software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo apt-key fingerprint 0EBFCD88
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt-get update
sudo apt-get install -y docker-ce docker-ce-cli containerd.io

sudo curl -L "https://github.com/docker/compose/releases/download/1.25.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```

If you have problems or have any other distribution, you should read the documentation - https://docs.docker.com/engine/install/ubuntu/.

On Windows and macOS you have to install and configure the Docker Desktop or you can use the Docker via WSL 2.


2) Register and log in at https://www.deezer.com - Unlike Spotify, it allows you to download music files in mp3 and flac format.

3) After logging in to the home page, press F12 (in Firefox) and go to the Storage tab and search and save to a text file the value of the `arl` variable (quite long about 195 characters).

![Heheszki](https://user-images.githubusercontent.com/41945903/83638574-a5ec3c00-a5a9-11ea-8002-2ff6f295842c.png)

4. Then create the `docker-compose.yml` configuration file anywhere and paste it into the file.

```
version: '3.7'

services:
  deemix:
    container_name: deemix
    image: registry.gitlab.com/bockiii/deemix-docker
    restart: unless-stopped
    ports:
      - "6595:6595"
    environment:
      - PUID=1000
      - PGID=1000
      - ARL=AAAAAAAAAAAAAAAAAAAAAAAAAA
    volumes:
      - /home/rafal/Place:/downloads
      - deemix-config-data:/config


volumes:
  deemix-data:
    name: deemix-data
  deemix-config-data:
    name: deemix-config-data
```

In this file you have to change `AAAAAAAAAAAAA to the previously copied `arl` value and instead of `/home/rafal/Place` select the path to which the newly downloaded songs should be saved.

Then, being in exactly the same folder, you can start the server using the `docker-compose up -d` command.

After about 1 minute (this may take a little longer) you can use the server at `http://localhost:6595/`.

![Heheszki](https://user-images.githubusercontent.com/41945903/83638000-c36cd600-a5a8-11ea-92a2-b7c1249af4c4.png)

8. You can now download any music to listen to it without any app.

9. For any questions or bugs should used subreddit - https://www.reddit.com/r/deemix
