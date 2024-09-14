# Geyser Standalone - Unofficial Docker image

[GeyserMC](https://geysermc.org/) allow clients from Minecraft Bedrock Edition to join your Minecraft Java server.
With this Docker image, you can launch a GeyserMC standalone server, to proxy your Minecraft Bedrock's players connection, to your Minecraft Java Edition server.

**This is an unofficial Docker Image originally developed by [Hiob](https://hiob.fr) for [Nefald Community](https://nefald.fr)**.

## Geyser: Documentation and setup
Always refer you to [GeyserMC documentation](https://github.com/GeyserMC/Geyser/wiki).

## Usage 
You can find support and updated documentation on our [Gitlab](https://git.nefald.fr/docker/geyser), also you can discuss and join us on our [Discord](https://nfald.fr/discord).

### Docker-compose
Here a sample of `docker-compose.yml` with **Geyser** and **Paper**:

```
version: '3.7'

services:
  geyser:
    image: tamikaschu/geyser:latest
    container_name: Geyser
    restart: unless-stopped
    stdin_open: true
    tty: true
    ports:
      - 19132:19132/tcp
      - 19132:19132/udp 
    volumes:
      - '/path/to/local/folder:/data:rw'
    environment:
      - OVERWRITE_CONFIG=false
      - BEDROCK_ADDRESS=0.0.0.0
      - BEDROCK_PORT=19132
      - BEDROCK_MOTD1=GeyserMC
      - BEDROCK_MOTD2="Minecraft server (GeyserMC)"
      - BEDROCK_SERVERNAME=ServerName
      - REMOTE_ADDRESS=PaperMC
      - REMOTE_PORT=25565      
      - REMOTE_AUTH_TYPE=floodgate    
```

### Environment variables
Please, refer to [GeyserMC wiki](https://github.com/GeyserMC/Geyser/wiki/Understanding-the-Config) for an update and complete understand of config. Environment variables are relate to config options.

| Variable | Default | Description |
|---|---|---|
| **INIT_MEMORY** | 1024M | Min memory allocated to GeyserMC. |
| **MAX_MEMORY** | 1024M | Max memory allocated to GeyserMC. |
| **OVERWRITE_CONFIG** | false | Overwrite config file with Docker run (or docker-compose) variables? |
| **BEDROCK_ADDRESS** | 0.0.0.0 | The address of Geyser on the bedrock end. |
| **BEDROCK_PORT** | 19132 | The port Geyser will run on. |
| **BEDROCK_CLONE_REMOTE_PORT** | false | Clone the remote port to the Bedrock client. |
| **BEDROCK_MOTD1** | Geyser | The first line of the MOTD for Geyser. |
| **BEDROCK_MOTD2** | Another Geyser server. | The second line of the MOTD for Geyser. |
| **BEDROCK_SERVERNAME** | Geyser | The world name that is shown in the top-right area of the pause screen. |
| **BEDROCK_COMPRESSION_LEVEL** | 6 | The compression level of the Bedrock connection. |
| **BEDROCK_BROADCAST_PORT** | 19133 | The port for broadcasting on Bedrock. |
| **BEDROCK_ENABLE_PROXY_PROTOCOL** | false | Whether to enable PROXY protocol or not for clients. |
| **REMOTE_ADDRESS** | auto | The address of the Minecraft: Java Edition server. |
| **REMOTE_PORT** | 25565 | The port of the Minecraft: Java Edition server. |
| **REMOTE_AUTH_TYPE** | online | The authentication type of the Minecraft: Java Edition server. |
| **REMOTE_USE_PROXY_PROTOCOL** | false | Whether to enable PROXY/HAProxy protocol or not while connecting to the server. |
| **REMOTE_FORWARD_HOSTNAME** | false | Forwards the hostname/IP address that the Bedrock client used to connect over to the Java server. |
| **GEYSER_FLOODGATE_KEY_FILE** | key.pem | The key file path for Floodgate. |
| **GEYSER_PENDING_AUTH_TIMEOUT** | 120 | The amount of time Geyser will wait for Bedrock clients to authenticate. |
| **GEYSER_COMMAND_SUGGESTIONS** | true | Enable or disable command suggestions. |
| **GEYSER_PASSTHROUGH_MOTD** | true | If the MOTD should be relayed from the remote server. |
| **GEYSER_PASSTHROUGH_PLAYER_COUNTS** | true | If the current and max player counts should be relayed from the remote server. |
| **GEYSER_PASSTHROUGH_INTERVAL** | 3 | How often to ping the remote server to update information, in seconds. |
| **GEYSER_FORWARD_PLAYER_PING** | false | If player ping should be forwarded to the Java server. |
| **GEYSER_MAX_PLAYERS** | 100 | The maximum number of players shown when pinging the server. |
| **GEYSER_DEBUG_MODE** | false | Enable or disable debug mode. |
| **GEYSER_SHOW_COOLDOWN** | title | Displays a fake cooldown message when players perform an action. |
| **GEYSER_SHOW_COORDINATES** | true | Shows coordinates on the Bedrock client. |
| **GEYSER_DISABLE_BEDROCK_SCAFFOLDING** | false | Disables scaffolding mechanics for Bedrock players. |
| **GEYSER_EMOTE_OFFHAND_WORKAROUND** | disabled | A workaround for Bedrock emote usage and item swapping. |
| **GEYSER_DEFAULT_LOCALE** | en_us | The default locale to send to players if their locale could not be found. |
| **GEYSER_CACHE_IMAGES** | 0 | Specify how many days images will be cached. |
| **GEYSER_ALLOW_CUSTOM_SKULLS** | true | Allows custom skulls to be displayed when placed. |
| **GEYSER_MAX_VISIBLE_CUSTOM_SKULLS** | 128 | The maximum number of visible custom skulls for Bedrock players. |
| **GEYSER_CUSTOM_SKULL_RENDERDISTANCE** | 32 | Render distance for custom skulls. |
| **GEYSER_ADD_NON_BEDROCK_ITEMS** | true | Adds non-Bedrock items to the game, like the furnace minecart. |
| **GEYSER_ABOVE_BEDROCK_NETHER_BUILDING** | false | Enables building above Y127 in the Nether. |
| **GEYSER_FORCE_RESOURCE_PACKS** | true | Forces clients to load resource packs. |
| **GEYSER_XBOX_ACHIEVEMENTS_ENABLED** | false | Allows Xbox achievements to be unlocked. |
| **GEYSER_LOG_PLAYER_IPS** | true | Logs player IPs on the server. |
| **GEYSER_NOTIFY_ON_UPDATE** | true | Notifies when an update is available. |
| **GEYSER_UNUSABALE_SPACE_BLOCK** | minecraft:barrier | The block used to fill unusable space. |
| **GEYSER_METRICS_ENABLED** | false | If metrics should be enabled. |
| **GEYSER_METRICS_UUID** | generateduuid | UUID of server, don't change! |
| **GEYSER_MTU** | 1400 | The maximum transmission unit size for packets. |
| **GEYSER_USE_DIRECT_CONNECTION** | true | Allows Bedrock players to connect directly to the server. |
| **GEYSER_DISABLE_COMPRESSION** | true | Disables compression for Bedrock clients. |



## LICENSE
This image is based on [nefald/geyser](https://hub.docker.com/r/nefald/geyser) (under MIT LICENSE).
