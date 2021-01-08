# Netdata installation on a Linux machine and data visualization with Grafana

> ROLAND Louis
> RAIMBAULT Florentin
> January 2021

**Please follow TO THE LETTER the Readme to install and use netdata with grafana !**

## Step 1 - Download and install a non-gui Debian virtual machine 

- Do not forget to use the bridge mode in network settings ! 
- You need to be root to run the services

## Step 2 - Install Docker and docker-compose

```
$ apt install docker.io curl git vim
$ curl -L "https://github.com/docker/compose/releases/download/1.27.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose```
$ chmod +x /usr/local/bin/docker-compose
```
*latest release of docker compose: https://github.com/docker/compose/releases/*

## Step 3 - Get the docker compose file and go to the folder downloaded

```
$ git clone https://github.com/l-roland/m3108-supervision.git
$ cd m3108-supervision
```

## Step 4 - Change power directory in docker-compose.yml and IP in prometheus/prometheus.yml file

```
$ pwd
$ vim docker-compose.yml
...
# put the result of the pwd command instead of pwd_result
pwd_result/prometheus/prometheus.yml:/etc/prometheus/prometheus.yml
```

```
$ vim m3108-supervision/prometheus/prometheus.yml
...
# put your ip address instead of ip_host
targets: ['ip_host:19999'] 
```

## Step 5 - Execute the docker compose

```
$ cd m3108-supervision/
$ docker-compose up or docker-compose up -d to run in background
```

## Step 6 - Services

- netdata : ip_host:19999
- metrics : ip_host:19999/api/v1/allmetrics?format=prometheus
- prometheus : ip_host:9090
- grafana : ip_host:3000

## Step 7 - Scrape data

- You can find here all parameters and metrics (=datas from netdata) you want : <ip_host>:19999/api/v1/allmetrics?format=prometheus

Parameter example : ```netdata_system_cpu_percentage_average{chart="system.cpu",family="cpu",dimension="system"}```

- Insert the parameter into prometheus to test

![](https://i.imgur.com/bsBU0d4.png)

## Step 8 - Add prometheus service in grafana

- Connect to grafana

```user=admin``` and ```password=grafana```

- Create a prometheus datasource

![](https://i.imgur.com/MSlxMPr.png)

## Step 9 - Create a graph with grafana

- Then create a dashboard and insert the parameter desired in Metrics

![](https://i.imgur.com/BX4NUVI.png)

- You can refresh with the value you want (Last 15 minutes and every 5 seconds)

![](https://i.imgur.com/FZo3uRQ.png)

- You can now watch you CPU usage in grafana !

![](https://i.imgur.com/UwN5vet.png)

- And also your avaible disk space and RAM : 

![](https://imgur.com/8sDC0V8.png)
