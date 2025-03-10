# greenplum-docker
Docker for greenplum (6) database.

## Build

```sh
docker build -t greenplum:6 .
```

or use apt-get mirror like `mirrors.aliyun.com`

```sh
docker build -t greenplum:6 . --build-arg APT_MIRROR=mirrors.aliyun.com 
```

## Single Node Docker

From the command line execute the following command:
```sh
docker run -it -p 5432:5432 --hostname=db_master_1 greenplum:6 bash
```

Connect to your host on port 5432 user/pass is gpadmin/dataroad

## Multi Node Docker-Compose

From the command line execute the following command: 
```sh
docker compose up
```

You can connect to your host using PGADMIN on port 5432 user/pass is gpadmin/dataroad

## Swarm Multi Node Docker-Compose

From the command line execute the following command: 
```sh
docker stack deploy -c docker-compose-stack.yml greenplum-stack
```

Deploy one segment for each docker swarm node
```sh
docker stack deploy -c docker-compose-swarm.yml greenplum-swarm
```

You can connect to your host using PGADMIN on port 5432 user/pass is gpadmin/dataroad

### singlehost

This file contains the name of the hosts to connect to. 
By default there is one host 'db_master_1'.
Will create two segment on one host

### multihost

This file contains the name of the segments that the master connects to. 
This is used when running a multi-node cluster and has 4 segments (each node have 2 segments) in it.

### gpinitsys

Configuration file for setting up the greenplum cluster.
By default each node has 2 segments.

More see [gpinitsystem](https://gpdb.docs.pivotal.io/6-16/utility_guide/ref/gpinitsystem.html)


## Variable

| Name | Type | Value |
|:-----:|:-----:|:-----:|
| GP_NODE | MUST | `master` for master, other for segment |
| GP_PASSWD | Optional | database password for user `gpadmin` |
| GP_SEG_DOMAIN | Optional | segment services domain, always prefix with `tasks.` and same with service name |
| HOSTFILE | Optional | hostfile of gpdb when use `gpinitsystem`, If you specify a file that does not exist, it will be automatically generated by looking for the real ip of each replicas of the docker service through the GP_SEG_DOMAIN variable |

## Questions?

chad@caoanalytics.com

[@xiaoyao9184](https://github.com/xiaoyao9184)


