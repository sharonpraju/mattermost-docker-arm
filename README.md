# Mattermost server for ARM (V7 or 64)

## How to run

1. Clone this repository
2. Create a .env file from .env.sample file
3. Modify environnement values
4. Create `mattermost` user in host machine with User ID and Group ID 2000.
   (If there is already a user existing with 2000 as ID, better use a different ID and update the same in .env file as well.)
   Replace 2000 with the value of PUID and PGID in .env file.
```
sudo groupadd -g 2000 mattermost
sudo useradd -u 2000 -g 2000 -M -d /nonexistent -s /sbin/nologin mattermost
```
5. Create the required directories and set their permissions.
   Replace 2000 with the value of PUID in .env file.
```
mkdir -p ./volumes/app/mattermost/{config,data,logs,plugins,client/plugins,bleve-indexes}
sudo chown -R 2000:2000 ./volumes
```

6. Up the stack ’docker-compose up -d’
7. Go to http://localhost:8065
   Replacce 8065 with MATTERMOST_HOST_PORT in .env file.

### Optional steps
1. To install custom plugin, custom plugin it should be enabled in volumes/app/mattermost/config/config.json (also change upload limit in the configuration if required).
Note: most of the custom plugins currently available does not work with ARM architecture.
2. Site URL must be set from System console in mattermost
3. To receive notification web socket need to be implemeted in the host server (Nginx/Apache) and Push Notification Server need to be configured in System console.
4. To hide the Preview mode banner and to receive emails from mattermost SMTP need to configured from System console.

## Troubleshootings

For issues related with permission (Permission denied)

Workaround :
```
sudo chown -R 2000:2000 ./volumes
docker-compose up --force-recreate
```
Replace 2000 with the value of PUID in .env file.

# Credits 

Original repository for source code : https://github.com/SmartHoneybee/ubiquitous-memory
<br>
Forked from : https://github.com/remiheens/mattermost-docker-arm
