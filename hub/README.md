Clow.Hub Maintenance
====================

## Start/Stop container

`docker stop hub`  
`docker start hub`  

## Upgrade image and container

`docker stop hub`  
`docker rm hub`  
`docker rmi clown/hub` or `docker rmi clown/rpi-hub`

Last step is `docker run` with all parameters as for initial setup.

## Start/Stop component

Get inside container: `docker exec -it bash`

`sc stop bridge`
`sc start bridge-simple`

## Add configuration for component

Edit relevant section in `/etc/supervisord.conf`

# Clown.Hub Components

## Clown.Universe - data representation, base functionalities

* Clown.Schema MQTT topic shema
* Clown.Model MQTT payload model
* Devices
    * Clown.Sensor
    * Clown.Actuator
* Clown.Interface - devices discovery, publish-interval configuration, etc.

## Docker Toolbox for desktop PC

[DockerToolbox-1.12.1.exe](https://github.com/docker/toolbox/releases/download/v1.12.1/DockerToolbox-1.12.1.exe)

* Docker v1.12.1
* boot2docker
* Git version 2.9.0
* Oracle VM VirtualBox 5.1.4

## Raspbian with Docker for Raspberry Pi

* [Hypriotos Version 1.0.0 Blackbeard](http://blog.hypriot.com/getting-started-with-docker-on-your-arm-device/)
* [RASPBIAN JESSIE LITE](https://www.raspberrypi.org/downloads/raspbian/)

## Clown.Hub Docker Image

* [Alpine Linux](https://www.alpinelinux.org/)
* [Supervisord process manager](http://supervisord.org/)
    * Configuration in /etc/supervisord.conf
* [Mosquitto MQTT broker](https://mosquitto.org/)
    * Configuration in /etc/mosquitto/mosquitto.conf
* [Caddy web server](https://caddyserver.com/)
    * Configuration in /etc/caddy.conf
* Tools
    * bash
    * mosquitto_pub, mosquitto_sub
    * wcat - simple WebSocker client
    * nano
* Clown.Hub
    * Python3 implementation in clow.* Python modules, executebles in /usr/bin
        * `hub` - Clown.Hub cli
        * `bridge-simple` - Simplified Python only interface Bridge - MQTT (disabled in default configuration)
        * `bridge-simulator` - Node simulator - publishes pseudorandom sensor measurements on topic nodes/bridge/simulator
        * `clown-talk-client` - stdin/stdout to MQTT - used for bc-bridge to publish on topic nodes/bridge/0
        * `clown-talk-server` - MQTT to stdin/stdout - used for web server to publish MQTT subtopics starting with configured base topic
    * `bc-bridge` - Clown.Talk Bridge server implemented in C
    * Clown.Dashboard - quick start web application for sensor monitoring and actuators control

Exposed are web server (80, 443) and MQTT broker (1883) TCP ports.

USB HID is accesible through shared \dev (\dev\hidraw*).

### Data store

`\var\hub` is exported to host system

#### Logs

`\var\hub\log`

#### MQTT data store

`\var\hub\data`

#### web server root

`\var\hub\www`

#### Clown.Plugin - Hub extensions

`\var\hub\plugins`
