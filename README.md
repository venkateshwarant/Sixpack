# Sixpack
Setting up the sixpack opensource tool for AB testing

## General overview
This tutorial shows how to setup Sixpack tool and run AB tests in [Web-based Hello World case study](https://github.com/acapozucca/helloworld).

## Assumptions/Pre-requisites

### Hardware
Laptop with at least 8 Gb memory (recommended 16 Gb, ideally 32 Gb)

### Software

1. **The Web-based Hello World case study**
* Instructions to install here: https://github.com/acapozucca/helloworld/blob/master/product.helloworld/README.md
* The product has to be deployed and tested whether it is available

2. **Redis-Server** (v3.0.6)
* Instructions to install here: https://redis.io/topics/quickstart
* Redis server has to be started before running the sixpack server as it relies on redis to store the data.

3. **Sixpack** 
* Instructions to install here: https://github.com/sixpack/sixpack

## Getting started
All the required packages are installed when we run the provided vagrant file. Once VM is created, ssh to the VM and follow the below steps.
 1. Start the Redis server by running the following command.
```
redis-server
```

2. In another tab, ssh to the VM and run the below command to start the sixpack client.
```
SIXPACK_CONFIG=/etc/sixpack/config.yml sixpack-web
```

3. In another tab, ssh inside the VM and run the below command to start the sixpack server.
```
SIXPACK_CONFIG=/etc/sixpack/config.yml sixpack
```

4. Once sixpack server, web, helloworld-product, and the redis server are started, we can check whether sixpack is working properly.

Access this link http://192.168.33.15:5001/ to access the dashboard of sixpack. It fails if the sixpack-web is not started properly.

5. If the sixpack web is working properly, access http://192.168.33.14:8080/helloworld/sixpack.html and check if the count is incremented in the sixpack panel. If incremented the sixpack is configured properly.

6. To check conversion rate, click the convert button and check if the corresponding count is incremented in the sixpack server.

7. To check if the data is properly put into redis, run the below command in side the VM.
```
redis-cli -n 15 KEYS '*'
```
Here, 15 refers to the DB number which we configured in the config.yml file.

## Background
Here, we will see how we configure the environment for sixpack to work properly.

1. First we to install the pip, because we will install some package through pip. For that we run the below command.
```
     sudo apt install python-pip -y
     pip install --upgrade pip
```

2. We install the sixpack with the below command.
```
pip install sixpack
```

3. We have to install redis since sixpack stores all the data in redis.
```
sudo apt-get install redis-server -y
```

4. We create a configuration file for sixpack. Its contents are
```
     redis_port: 6379                            # Redis port
     redis_host: localhost                       # Redis host
     redis_prefix: sixpack                       # all Redis keys will be prefixed with this
     redis_db: 15                                # DB number in redis
     metrics: false                              # send metrics to StatsD (response times, # of calls, etc)?
     statsd_url: 'udp://localhost:8125/sixpack'  # StatsD url to connect to (used only when metrics: true)
     # The regex to match for robots
     robot_regex: $^|trivial|facebook|MetaURI|butterfly|google|amazon|goldfire|sleuth|xenu|msnbot|SiteUptime|Slurp|WordPress|ZIBB|ZyBorg|pingdom|bot|yahoo|slurp|java|fetch|spider|url|crawl|oneriot|abby|commentreader|twiceler
     ignored_ip_addresses: []                    # List of IP
     asset_path: gen                             # Path for compressed assets to live. This path is RELATIVE to sixpack/static
     secret_key: 'test'        # Random key (any string is valid, required for sixpack-web to run)
```
