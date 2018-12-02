# Docker Downloader for seedbox.io

This docker set up allows you to set up a local dockerized Sonarr, Radarr, Jackett, Resilio Sync and Ombi that will automatically hook up to your seedbox.io seedbox instance, straight out of the box. You can then request media thorugh Ombi and invite your friends.

### Caveat:

**Warning:** This whole README uses $SEEDHOST in place of your seedbox link (e.g. psv23232.seedbox.io). Anywhere you see that, change it to your seedbox.io hostname.


# Installation

* [Setup Docker on the pi](https://blog.hypriot.com/getting-started-with-docker-and-linux-on-the-raspberry-pi/)

* [Setup Docker-Compose](https://www.berthon.eu/2017/getting-docker-compose-on-raspberry-pi-arm-the-easy-way/)

* Download [docker-compose.yml](https://raw.githubusercontent.com/Fredddi43/seedboxio-docker-downloader-raspberry/master/docker-compose.yml) from this repo to a folder where you can execute it (e.g. /opt/, if you're root)

* Checkout [Ombi](https://github.com/linuxserver/docker-ombi-armhf) to the root of the same folder

* Execute "docker-compose up -d" and let it build Ombi and pull the images for the others

* While you wait, visit $SEEDHOST/dav  and create a directory called `CompletedDownloads`

* Open $SEEDHOST  and click on the settings icon. Go to "Autotools". Make sure AutoMove is checked, if torrent's label matches filter /.*/ with the directory, /home/psv23232/files/CompletedDownloads. Also check the "Add torrent's label to path"

![rTorrent Settings](https://github.com/hjhart/docker-downloader/blob/master/assets/rtorrent_settings.png)

Now go add the `CompletedDownloads` directory.

* Visit $SEEDHOST/resilio and add that directory in Resilio Sync, copy the read-write secret.

* Visit 0.0.0.0:8888 and setup a local folder for CompletedDownloads by clickong the "+", then "enter a link".

## Configure Radarr:

* Add indexers that you want to add. (Jackett can be configured / found on port 9117)
* Add rTorrent as a Download Client to point to your seedbox.io. [See this article](https://panel.seedbox.io/index.php?rp=/knowledgebase/41/How-to-connect-Sonarr-to-your-service.html)
* Toggle "Advanced Settings" in the Download Client tab.
* Add a new Remote Path Mapping like this:

```
   host                               remote path                                        local path
$SEEDHOST                        /home/psv23232/files/                                       /downloads/radarr/

```

## Configure Sonarr: 

* Add indexers that you want to add. (Jackett can be configured / found on port 9117)
* Add rTorrent as a Download Client to point to your seedbox.io. [See this article](https://panel.seedbox.io/index.php?rp=/knowledgebase/41/How-to-connect-Sonarr-to-your-service.html)
* Toggle "Advanced Settings" in the Download Client tab.
* Add a new Remote Path Mapping like this:

```
   host                               remote path                                        local path
$SEEDHOST                        /home/psv23232/files/                                       /downloads/tv-sonarr/

```
## Configure Ombi:

* [Follow any guide, no special settings here](https://github.com/Cloudbox/Cloudbox/wiki/Install:-Ombi)


## Congratulations!

Now you should be all set up. If you have any problems, leave an issue in github and I'll get back to you.

