# English words

~~~shell
parcel   # 包

parquet # 实木复合地板 ，Apache Parquet is a columnar storage format available to any project in the Hadoop ecosystem, regardless of the choice of data processing framework, data model or programming language.

Topology # 拓扑

credo  # 信条

elaborate  # 阐述  来自Kafka官网

payload  # 有效载荷

ingest  # 捏取

condensed # 冷凝


purge # 清除

~~~





~~~shell
curl -X POST -H 'Content-Type: application/json' -i 'http://192.168.1.30:8083/connectors' --data '{"name":"load-mysql-data","config":{"connector.class":"JdbcSourceConnector","connection.url":"jdbc:mysql://192.168.1.212:3306/connector?user=root","mode":"timestamp","validate.non.null":"false","timestamp.column.name":"login_time","table.whitelist":"login","mode":"timestamp","topic.prefix": "mysql."}}'


curl -X POST -H 'Content-Type: application/json' -i 'http://localhost:8083/connectors' --data '{"name":"load-mysql-data","config":{"connector.class":"JdbcSourceConnector","connection.url":"jdbc:mysql://localhost:3306/connector?user=root&password=isea","mode":"timestamp","validate.non.null":"false","timestamp.column.name":"login_time","table.whitelist":"login","mode":"timestamp","topic.prefix": "mysql."}}'


curl -X POST -H 'Content-Type: application/json' -i 'http://localhost:8083/connectors' --data '{"name":"sink-data-2mysql","config":{"connector.class":"JdbcSinkConnector","connection.url":"jdbc:mysql://localhost:3306/connector?user=root&password=isea","topics":"","name": "jdbc-sink"}}'


~~~

