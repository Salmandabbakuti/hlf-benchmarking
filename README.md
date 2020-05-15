# hlf-benchmarking
Hyperledger fabric network benchmarking with caliper.

> Note: Make sure your network is up and running.

#### Setup
###### 1. Network configuration:

###### 3. Mounting Network and benchmark configurations to caliper container
```
services:
  caliper:
    container_name: caliper
    image: hyperledger/caliper:0.3.0
    command: launch master
    environment:
      - CALIPER_BIND_SUT=fabric:1.4.4
    network_mode: host
    ```
    

```
###### 4. Starting Tests

```
docker-compose -f docker-compose-caliper.yaml up -d

docker-logs -f caliper # observe logs of caliper. it would take a while to finish based on your network and your pc.
```

###### 5. Report


