<h1 align='center'>TeamSpeak 3 Server Installer</h1>

#### Run as root those commands to update and upgrade all installed packages on your server:
```
apt-get update
apt-get upgrade
apt-get dist-upgrade
```
#### Create a new user for your Teamspeak3 server (press ENTER for all questions):
```
adduser --disabled-login teamspeak
```
#### Login as teamspeak user:
```
cd /home/teamspeak/; su teamspeak
```
#### Download and extract the last version:
```
wget https://github.com/Mursin-Doankk/ts3linux/raw/main/teamspeak3-server_linux_amd64-3.13.7.tar.bz2
tar xvfj teamspeak3-server_linux_amd64-3.13.7.tar.bz2
cd teamspeak3-server_linux_amd64
cp * -R /home/teamspeak
cd ..
rm -r teamspeak3-server_linux_amd64
rm -f teamspeak3-server_linux_amd64-3.13.7.tar.bz2
```
#### Start your server for the first time (save login details and secret key to claim the server in TeamSpeak app)
```
./ts3server_startscript.sh start
```
#### To stop the script press CTRL+C

#### Now let's create the start script:
```
nano /lib/systemd/system/ts3server.service
```
#### add in the file:
```
[Unit]
Description=Teamspeak Service
Wants=network.target

[Service]
WorkingDirectory=/home/teamspeak
User=teamspeak
ExecStart=/home/teamspeak/ts3server_minimal_runscript.sh
ExecStop=/home/teamspeak/ts3server_startscript.sh stop
ExecReload=/home/teamspeak/ts3server_startscript.sh restart
Restart=always
RestartSec=15

[Install]
WantedBy=multi-user.target
```
#### save the file  CTRL and X together, then Press Y).

#### To enable it run at server boot:
```
systemctl enable ts3server.service
```
#### Reboot the server and check if your TeamSpeak server is running:
```
systemctl status ts3server
```
#### if you have in the ouput Active: active (running) your server is ready!
```
sudo ufw allow 3033/tcp
sudo ufw allow 9987/udp
sudo ufw allow 1011/tcp
```
#### Enjoy your server!
