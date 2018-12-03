# Druid 

## Start up Zookeeper

```
curl http://www.gtlib.gatech.edu/pub/apache/zookeeper/zookeeper-3.4.10/zookeeper-3.4.10.tar.gz -o zookeeper-3.4.10.tar.gz
tar -xzf zookeeper-3.4.10.tar.gz
cd zookeeper-3.4.10
cp conf/zoo_sample.cfg conf/zoo.cfg
./bin/zkServer.sh start
```

## Start up Druid services

```
bin/init
```

This will setup up some directories for you. Next, you can start up the Druid processes in different terminal windows. This tutorial runs every Druid process on the same system. In a large distributed production cluster, many of these Druid processes can still be co-located together.

```
java `cat examples/conf/druid/coordinator/jvm.config | xargs` -cp "examples/conf/druid/_common:examples/conf/druid/_common/hadoop-xml:examples/conf/druid/coordinator:lib/*" io.druid.cli.Main server coordinator
java `cat examples/conf/druid/overlord/jvm.config | xargs` -cp "examples/conf/druid/_common:examples/conf/druid/_common/hadoop-xml:examples/conf/druid/overlord:lib/*" io.druid.cli.Main server overlord
java `cat examples/conf/druid/historical/jvm.config | xargs` -cp "examples/conf/druid/_common:examples/conf/druid/_common/hadoop-xml:examples/conf/druid/historical:lib/*" io.druid.cli.Main server historical
java `cat examples/conf/druid/middleManager/jvm.config | xargs` -cp "examples/conf/druid/_common:examples/conf/druid/_common/hadoop-xml:examples/conf/druid/middleManager:lib/*" io.druid.cli.Main server middleManager
java `cat examples/conf/druid/broker/jvm.config | xargs` -cp "examples/conf/druid/_common:examples/conf/druid/_common/hadoop-xml:examples/conf/druid/broker:lib/*" io.druid.cli.Main server broker
```

## Ingestion Command

```
curl -X 'POST' -H 'Content-Type:application/json' -d @query/________.json http://localhost:8090/druid/indexer/v1/task

curl -X 'POST' -H 'Content-Type:application/json' -d @query/________.json http://localhost:8082/druid/v2/sql
```


