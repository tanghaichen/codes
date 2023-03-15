# 1 创建kafka主题。
  ```./bin/kafka-topics.sh --create --bootstrap-server ip:9092  --topic 主题名(不可存在下划线）;```
# 2 创建clickhou源表。
## a.创建接kafka接收源表
此表不可打开，查询一次后就会清空
``` 
CREATE TABLE 表名source ( `id` String COMMENT '唯一ID' )
ENGINE = Kafka () 
SETTINGS kafka_broker_list = 'kafkaip:9092',
kafka_topic_list = '主题',
kafka_group_name = '消费者组',
kafka_format = 'JSONEachRow';
```
## b.创建接kafka目标表
此表不可打开，查询一次后就会清空
``` 
CREATE TABLE 表名target ( `id` String COMMENT '唯一ID' )
ENGINE = Kafka () 
ENGINE = MergeTree() PARTITION BY toYYYYMM(ts
```

# 3 创建物化视图。
```
CREATE MATERIALIZED VIEW 视图名 TO 表名target AS SELECT * FROM 表名source;
```
源表将实时接收kafka数据并通过视图同步到目标表中。目标表为业务表进行处理
