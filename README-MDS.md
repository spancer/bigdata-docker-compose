# Modern data stack deployment using docker compose
Deploy modern data stack using docker compose, you can use docker to set up s3 based big data platform in a few minutes.

## How to build ?
Docker build files are holded [here](https://github.com/spancer/bigdata-docker-builds.git), you can folk and customize as needed.

## Supported components

* Hive Metastore 3.1.2
* TrinoDB 395+
* Kafka 2+
* Flink 1.16.1
* Iceberg 1.1.0
* Minio
## How to Run

Git clone the repo and run docker-compose.

    docker-compose -f docker-compose-mds.yaml up -d

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

## How to visit services in web ui?

* Minio: http://minio:9001/
* Trino: http://trinodb:8080/
* Flink:http://jobmanager:8081/ 
```
Note: you have to add the server ip and services (which defined in docker-compose.yml) to your local hosts firstly. [how to configure hosts](https://www.howtogeek.com/howto/27350/beginner-geek-how-to-edit-your-hosts-file/)


