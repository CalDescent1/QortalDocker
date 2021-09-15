# Dockerized Qortal Testnet Node

Run one or more Qortal testnet nodes on a single host.

## Basic usage

Build the docker image:
```
./build.sh
```

Create some container instances, in this case 3:
```
./run.sh 3
```

The first container will use ports 62401 and 62402. Each additional container will increase these by 10, so the second would use 62411 and 62412, the third would use 62421 and 62422, etc.


List the running containers:
```
docker container ls | grep qortal
```

The network port of each running container can be seen in the name, after `qortal_`, e.g. `qortal_62402`


Tail the logs of the container instance with network port 62402:
```
./logs.sh 62402
```


Add a minting key to the container instance with network port 62402:
```
./add_minting_key.sh 62402 <reward_share_priv_key>
```

Stop and remove container with network port 62402:
```
./stop.sh 62402
```

Or alternatively, stop and remove all Qortal containers:
```
./stop.sh all
```

Data is persisted in a volume named `qortal_<netport>`, so running a new container on a previously used port will use an existing copy of the database and log files. To clear this data and start from a clean set of files, stop the instance, then run this command, substituting 62402 for the network port of the node you'd like to clear data for:
```
docker volume rm qortal_62402
```
