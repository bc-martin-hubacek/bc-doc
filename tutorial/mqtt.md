# MQTT - Message transfer protocol

## MQTT Basics

- Simple, Lightweight and open message protocol
- Each message consists of **topic** and **payload**
- Topic is describing the meaning of the data in payload. Topic uses tree-like structure with "/" symbol. Example topics: "bedroom/temperature", "kitchen/light/set"
- MQTT server is called **Broker** and clients can **publish** messages and **subscribe** to different types of topics
- In subscribe topics the wildcard "+" can be used for single level subscription and symbol "#" for multi level subscribtion. [More on topics](http://www.hivemq.com/blog/mqtt-essentials-part-5-mqtt-topics-best-practices)

## Mosquitto MQTT broker

BigClown uses opensource [Mosquitto](https://mosquitto.org/) broker which is running inside Docker.

To test MQTT and see the sent messages you can subscribe to topic with

`docker exec hub mosquitto_sub -v -t 'nodes/bridge/0/#'`

If you would like to connect from outside of the docker or from different machine, you can remove the `docker exec hub` and add `-h <ip/host>` parameter of the address of running broker.

To publish a message you use **mosquitto_pub** command

`docker exec hub mosquitto_pub -t nodes/bridge/0/relay/i2c0-3b/set -m '{"state": true}'`

Configuration file is located in `/etc/mosquitto/mosquitto.conf`
