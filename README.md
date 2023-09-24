# learn-kafka

## cluster conf
```ini
auto.create.topics.enable=true
default.replication.factor=2
min.insync.replicas=2
num.io.threads=8
num.network.threads=5
num.partitions=1
num.replica.fetchers=2
replica.lag.time.max.ms=30000
socket.receive.buffer.bytes=102400
socket.request.max.bytes=104857600
socket.send.buffer.bytes=102400
unclean.leader.election.enable=true
zookeeper.session.timeout.ms=18000
log.retention.ms=10000
log.segment.bytes=2147483647
```

## s3connector conf
```ini
connector.class=io.confluent.connect.s3.S3SinkConnector
s3.region=ap-northeast-2
partition.duration.ms=1000
topics.dir=logs
flush.size=3
tasks.max=1
topics=orders
timezone=Asia/Seoul
locale=ko_KR
format.class=io.confluent.connect.s3.format.bytearray.ByteArrayFormat
partitioner.class=io.confluent.connect.storage.partitioner.TimeBasedPartitioner
value.converter=org.apache.kafka.connect.converters.ByteArrayConverter
storage.class=io.confluent.connect.s3.storage.S3Storage
s3.bucket.name=wsi-result-objects
path.format=YYYY/MM/dd/HH
```

## datagen conf
```ini
connector.class=io.confluent.kafka.connect.datagen.DatagenConnector
quickstart=orders
tasks.max=1
value.converter.schemas.enable=false
kafka.topic=orders
value.converter=org.apache.kafka.connect.json.JsonConverter
max.interval=10000
key.converter=org.apache.kafka.connect.storage.StringConverter
iterations=-1
```

## rds conf
```ini
connector.class=io.debezium.connector.mysql.MySqlConnector
schema.history.internal.consumer.sasl.client.callback.handler.class=software.amazon.msk.auth.iam.IAMClientCallbackHandler
database.user=admin
schema.history.internal.producer.sasl.client.callback.handler.class=software.amazon.msk.auth.iam.IAMClientCallbackHandler
database.server.id=184054
tasks.max=1
schema.history.internal.consumer.sasl.jaas.config=software.amazon.msk.auth.iam.IAMLoginModule required;
database.server.name=dev
schema.history.internal.kafka.bootstrap.servers=b-1.wsicluster.suf97u.c4.kafka.ap-northeast-2.amazonaws.com:9098,b-2.wsicluster.suf97u.c4.kafka.ap-northeast-2.amazonaws.com:9098
include.schema.changes=true
database.port=3306
topic.prefix=order3-
schema.history.internal.kafka.topic=orders2
schema.history.internal.producer.security.protocol=SASL_SSL
database.hostname=wsi-db.cluster-cadxb1cncc5b.ap-northeast-2.rds.amazonaws.com
database.password=password
schema.history.internal.consumer.sasl.mechanism=AWS_MSK_IAM
schema.history.internal.producer.sasl.jaas.config=software.amazon.msk.auth.iam.IAMLoginModule required;
schema.history.internal.producer.sasl.mechanism=AWS_MSK_IAM
schema.history.internal.consumer.security.protocol=SASL_SSL
```

## s3 source conf
```ini
connector.class=io.confluent.connect.s3.source.S3SourceConnector
mode=GENERIC
s3.region=ap-northeast-2
topics.dir=
format.class=io.confluent.connect.s3.format.json.JsonFormat
confluent.topic.bootstrap.servers=b-1.wsicluster.suf97u.c4.kafka.ap-northeast-2.amazonaws.com:9098,b-2.wsicluster.suf97u.c4.kafka.ap-northeast-2.amazonaws.com:9098
tasks.max=1
value.converter.schemas.enable=false
value.converter=org.apache.kafka.connect.json.JsonConverter
topic.regex.list=orders:.*
s3.bucket.name=wsi-source-objects
```
