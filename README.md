# kkk
apt-get update ; apt-get upgrade -y ; apt-get install docker.io mc irssi nano; adduser misio ; usermod -a -G sudo misio

apt-get install screen mc irssi

mkdir -p /home/misio/kkk/torr && mkdir /home/misio/kkk/finito; cd ~/.irssi/ && mkdir scripts && cd scripts && mkdir autorun && cd autorun && wget http://scripts.irssi.org/scripts/dccstat.pl && mkdir /home/misio/mirc && cd /home/misio && irssi

/statusbar dccstat add dccstat
/set dcc_autoget ON
/set dcc_autoresume ON
/set dcc_download_path /tmp/mirc/
/server add -auto -network fn irc.abjects.net
/network add -nick BearimusPrime -autosendcmd "/msg NickServ identify jackass1" fn
/channel add -auto #moviegods fn
/channel add -auto #mg-chat fn
/channel add -auto #mg-lounge fn
/server add -auto -network horr irc.rizon.net
/network add -nick NedvedPL -autosendcmd "/msg NickServ identify jackass1" horr
/channel add -auto #horriblesubs horr
/ignore #horriblesubs MODES JOINS PARTS QUITS
/ignore #moviegods MODES JOINS PARTS QUITS
/ignore #mg-chat MODES JOINS PARTS QUITS
/ignore #mg-lounge MODES JOINS PARTS QUITS
/save
/quit

mkdir -p /root/.config/rclone && cd /root/.config/rclone && wget ftp://nedpl:jackass1@ftp.drivehq.com/rclone.conf && curl https://rclone.org/install.sh | sudo bash

curl -fsSL https://get.docker.com -o get-docker.sh && sh get-docker.sh

kkk.yml:
version: "2.1"
services:
  jellyfin:
    image: lscr.io/linuxserver/jellyfin:latest
    container_name: jellyfin
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Etc/UTC
      - JELLYFIN_PublishedServerUrl=192.168.0.5 #optional
    volumes:
      - /tmp/mirc/filmy:/data/movies
      - /tmp/mirc/seriale:/data/shows
    ports:
      - 8096:8096
      - 8920:8920 #optional
      - 7359:7359/udp #optional
      - 1900:1900/udp #optional
    restart: unless-stopped

docker compose -f kkk.yml up -d

usermod -a -G users misio && usermod -a -G sudo misio && usermod -a -G docker misio && usermod -a -G misio misio && echo '* *     * * *   root    /home/misio/skrypt.sh' >> /etc/crontab && cd /home/misio && docker run -d --init --restart=always -v /tmp/mirc/downloads/:/opt/JDownloader/Downloads -v /home/misio/config/:/opt/JDownloader/app/cfg --name jdownloader -u $(id -u) -p 3129:3129 -e MYJD_USER=dziwak9@gmail.com -e MYJD_PASSWORD=jackass1 -e MYJD_DEVICE_NAME=Misio jaymoulin/jdownloader && wget ftp://nedpl:jackass1@ftp.drivehq.com/skrypt.sh && chmod +x skrypt.sh && mkdir ggg && chmod 777 -R /tmp/mirc


import subprocess
from time import sleep
print('siema')

while True:
    rc = subprocess.call('/home/misio/skrypt.sh')
    sleep(30)
