# hlf-benchmarking
Hyperledger fabric network benchmarking with caliper.

> Note: Make sure your network is up and running.

#### Setup
###### 1. Network configuration:
- Inorder to benchmark your network, caliper should be connected with your running network. So we need to define our network(peers,orderers and their endpoints, channels, chancodes).
- Place your network's ```crypto-config``` directory into ```./caliper/networks/basic-network/``` directory.
- Sample network configuration file can be found in ```./caliper/networks/basic-network/network-config.yaml```
>Note: If you're network has tls enabled, you should also define tlscerts in ```network-config.yaml```

###### 2. Benchmarking Configuration:
- Once caliper succesfully connected to your network, it will look for the benchamark configuration file to execute transactions. so we need to define what chaincode functions to be executed and number of rounds, no.of transactions in a round etc. to check the performance of your network efficiently.
- Sample benchmark config file can be found in ```./caliper/benchmarks/mycc/```

###### 3. Mounting Network and benchmark configurations to caliper container
```
services:
  caliper:
    container_name: caliper
    image: hyperledger/caliper:0.3.0
    command: launch master
    environment:
      - CALIPER_BIND_SUT=fabric:1.4.4
      - CALIPER_BENCHCONFIG=benchmarks/mycc/config.yaml
      - CALIPER_NETWORKCONFIG=networks/basic-network/network-config.yaml
    volumes:
      - ./caliper:/hyperledger/caliper/workspace
    network_mode: host
    ```
    

```
###### 4. Starting Tests

```
docker-compose -f docker-compose-caliper.yaml up -d

docker-logs -f caliper # observe logs of caliper. it would take a while to finish based on your network and your pc.
```

###### 5. Report

- Once benchmarking is completed, Your network report will be generated in ```./caliper``` directory as ```report.html```. open it in your browser and check your fabric network performance.


