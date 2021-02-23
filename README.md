# Bigdata with docker compose
Deploy big data components using docker compose. 

## Supported components

* Apache Hadoop 3.2
* Prestodb 0.247
* Kafka 2+
* Hbase 2.2
* Hive 3.1.2
* ELK 7.9.1
## How to Run

Git clone the repo and run docker-compose.

    docker-compose up -d

## How to setup docker & docker compose

Install  docker ce on centos 7 or above:
```
1. yum remove docker docker-common docker-selinux docker-engine
2. yum install -y yum-utils device-mapper-persistent-data lvm2
3. yum-config-manager --add-repo https://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
4. yum install -y docker-ce
5. systemctl start docker.service
6. systemctl enable docker.service

```

Install docker-compose:
```
1. sudo curl -L "https://github.com/docker/compose/releases/download/1.23.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

2. sudo chmod +x /usr/local/bin/docker-compose

3. docker-compose --version
```

## How to test prestodb to confirm whether it works?
```
1. cd the prestodb container: docker-compose exec prestodb bash
2. connect to presto using presto-client: presto --server prestodb:8080 --catalog elasticsearch 
3. query some data: show schemas; show tables; select * from nodes;
4. you can also verify presto status through web ui: http://your-host-ip:9999
```

## ToDo
1. Integration flink 1.12
2. ~~Integration hive 3.1 (Done)~~
3. Integration hbase 2.2
4. Integration iceberg
5. Integration alluxio
6. Integration ozone