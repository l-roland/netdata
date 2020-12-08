# Netdata installation on a Linux machine and data visualization with Grafana

> ROLAND Louis
> RAIMBAULT Florentin
> December 2020

## Install Docker and docker-compose

```
$ apt install docker.io curl git
$ curl -L "https://github.com/docker/compose/releases/download/<latest_release>/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

*<latest_release> : https://github.com/docker/compose/releases/*

## Get the docker compose file

```
$ git clone https://github.com/l-roland/m3108-supervision.git
```

## Change IP in prometheus/prometheus.yml file

```
$ vim m3108-supervision/prometheus/prometheus.yml

-> targets: ['<ip_host>:19999'] # put your ip address in <ip_host>
```

## Execute the docker compose

```
$ cd m3108-supervision/
$ docker-compose up
```

## Services

- netdata : <ip_host>:19999
- metrics : <ip_host>:19999/api/v1/allmetrics?format=prometheus
- prometheus : <ip_host>:9090
- grafana : <ip_host>:3000

## Scrape data

- You can find here all parameters and metrics (=datas from netdata) you want : <ip_host>:19999/api/v1/allmetrics?format=prometheus

Parameter example : ```netdata_system_cpu_percentage_average{chart="system.cpu",family="cpu",dimension="system"}```

- Insert the parameter into prometheus to test

![](https://i.imgur.com/bsBU0d4.png)

## Add prometheus service in grafana

- Connect to grafana

```user=admin``` and ```password=grafana```

- Create a prometheus datasource

![](https://i.imgur.com/MSlxMPr.png)

## Create a graph with grafana

- Then create a dashboard and insert the parameter desired in Metrics

![](https://i.imgur.com/BX4NUVI.png)

- You can refresh with the value you want (Last 15 minutes and every 5 seconds)

![](https://i.imgur.com/FZo3uRQ.png)

- You can now watch you CPU usage in grafana !

![](https://i.imgur.com/UwN5vet.png)
