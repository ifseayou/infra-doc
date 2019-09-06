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





~~~:two_hearts:
curl -X POST -H 'Content-Type: application/json' -i 'http://192.168.1.30:8083/connectors' --data '{"name":"load-mysql-data","config":{"connector.class":"JdbcSourceConnector","connection.url":"jdbc:mysql://192.168.1.212:3306/connector?user=root","mode":"timestamp","validate.non.null":"false","timestamp.column.name":"login_time","table.whitelist":"login","mode":"timestamp","topic.prefix": "mysql."}}'







{"error_code":400,"message":"Connector configuration is invalid and contains the following 2 error(s):\nInvalid value java.sql.SQLException: Unknown error 1045 for configuration Couldn't open connection to jdbc:mysql://192.168.1.212:3306/connector?user=root\nInvalid value java.sql.SQLException: Unknown error 1045 for configuration Couldn't open connection to jdbc:mysql://192.168.1.212:3306/connector?user=root\nYou can also find the above list of errors at the endpoint `/{connectorType}/config/validate`"}
~~~

