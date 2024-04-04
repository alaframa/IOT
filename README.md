# IOT
THIS PROJECT IS TO MAKE IOT PLATFORM AT YOUR SERVER

the tech need to use is 
ubuntu > docker > mqtt eclips, portainer, etc
this is my 1st documenta tion so be it


##1st make a file compose

```
version: '3'

services:
  mariadb:
    image: mariadb:latest
    ports:
      - "3306:3306"
    environment:
      MYSQL_ROOT_PASSWORD: none
    restart: unless-stopped

  adminer:
    image: adminer
    ports:
      - "8080:8080"
    links:
      - mariadb:db
    restart: unless-stopped

  grafana:
    image: grafana/grafana:latest
    ports:
      - "3000:3000"
    restart: unless-stopped

  influxdb:
    image: influxdb:latest
    ports:
      - "8086:8086"
    volumes:
      - ${PWD}/sandbox/influxdb:/var/lib/influxdb2
    restart: unless-stopped

  mqtt-server:
    image: eclipse-mosquitto
    ports:
      - "1883:1883"
      - "9001:9001"
    volumes:
      - ${PWD}/sandbox/mqtt/mosquitto.conf:/mosquitto/config/mosquitto.conf
      - ${PWD}/sandbox/mqtt/mosquitto.passwd:/mosquitto/config/mosquitto.passwd
      - ${PWD}/sandbox/mqtt/data:/mosquitto/data
      - ${PWD}/sandbox/mqtt/log:/mosquitto/log
    restart: unless-stopped

  nodered:
    image: nodered/node-red:latest
    ports:
      - "1880:1880"
    volumes:
      - ${PWD}/sandbox/nodered/nodered_data:/data
    restart: unless-stopped

```
