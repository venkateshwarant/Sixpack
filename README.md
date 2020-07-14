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
