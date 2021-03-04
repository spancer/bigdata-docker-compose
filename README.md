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

## How to visit services in web ui?

* HDFS: http://namenode:9870/
* YARN: http://resourcemanager:8088/
* ES：http://elasticsearch:9200/
* Kibana:http://kibana:5601/
* Presto: http://prestodb:9999/
* Hbase: http://hbase-master:16010/
* Flink:http://jobmanager:8081/ (you have to start a yarn-session firstly)
```
Note: you have to add the server ip and services (which defined in docker-compose.yml) to your local hosts firstly. [how to configure hosts](https://www.howtogeek.com/howto/27350/beginner-geek-how-to-edit-your-hosts-file/)

## Produce some data to test HDFS & Hive

 <pre>
   create a table in hive:

   ```hive sql
   create external table test(
    id      int
   ,name    string
   ,skills   array<string>
   ,add     map<String,string>
    )
    row format delimited
    fields terminated by ','
    collection items terminated by '-'
    map keys terminated by ':'
    location '/user/test'
   ```
   </pre>

<pre>

create a txt file with the content below, put it under /data/ directory, such as
/data/example.txt

```
1,spancer,bigdata-ai-devops,changsha:lugu-changsha:chuanggu
2,jack,webdev-microservices,shenzhen:nanshan-usa:la
3,james,android-flutter,beijing:chaoyang
3,james,ios-flutter,beijing:chaoyang
```
</pre>

<pre>

load local file data into the external hive table, which we created above.

```
load data local inpath ‘/tools/example.txt’ overwrite into table test; 

```
</pre>


<pre>

Check the mr job in yarn web ui :http://resourcemanager:8088/

After the job is done, query in hive client. Alternative, we can query the data in presto client.

```
select * from test;
```
</pre>


## How to test prestodb to confirm whether it works?
```
1. cd the prestodb container: docker-compose exec prestodb bash
2. connect to presto using presto-client: presto --server prestodb:8080 --catalog elasticsearch 
3. query some data: show schemas; show tables; select * from nodes;
4. you can also verify presto status through web ui: http://your-host-ip:9999
```
## Run jobs on the docker platform.

For java developers, I provide some tests over the platform. You can fork it from [here](https://github.com/spancer/flink-iceberg-demo), the test project
contains flink jobs with set of components, such as kafka, elasticsearch, iceberg, etc.. Source and sink examples are fully inclued.

## ToDo
1. Integration flink 1.12
2. ~~Integration hive 3.1 (Done)~~
3. ~~Integration hbase 2.2~~
4. ~~Integration iceberg~~
5. Integration alluxio
6. Integration ozone
