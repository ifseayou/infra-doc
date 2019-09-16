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

supervisor   # 监工

~~~







~~~properties
#--------------translator配置---------------#
kafka.bootstrap.servers = M1:9092,M2:9093,S1:9094
translator.kafka.source.topics = seconddata-topic
translator.kafka.application.name = translatorTest
translator.kafka.sink.topic = prodadapter-topic
translator.kafka.consume.poll = 300
translator.envirType = IOE

redis.host = 192.168.1.212
redis.port = 6379
redis.timeout = 2000
redis.password = sys
redis.database = 5

#--------------event.distribute配置---------------#
event.distribute.application.id = event-distributeTest
event.distribute.kafka.source.topics = eventdata-topic
#该配置生产环境没有
event.distribute.num.stream.threads = 2
## 事件分发相关配置
event.distribute.warn.topic = secwarndata-topic
event.distribute.switch.topic = switchdata-topic
event.distribute.other.topic = othereventdata-topic

event.distribute.logging.file = event-distribute/logs/event-distribute.log
logging.level.com.joinbright = info

#--------------warn配置---------------#
# Kafka streams项目的ID，用作Group ID.
warn.application.id = warn-sec

# 规则缓存刷新时间，单位是秒
warn.cache.flush.interval = 5
# 作为程序输入的Kafka topic
warn.kafka.source.topics = seconddata-topic
# 作为程序输出的Kafka topic
warn.kafka.sink.topic = secwarndata-topic
warn.num.stream.threads = 1

#================================ Redis =====================================
redis.common.host = 192.168.1.212
redis.common.port = 6379
redis.common.password = sys
redis.common.database = 5
redis.common.timeout = 2000
redis.common.maxTotal = 200
redis.common.maxWaitMillis = 15000
redis.common.testOnBorrow = true
redis.common.maxIdle = 100
#================================ Rule =====================================
spark.steaming.rule.param.prefix = $
# 告警规则类别，m:分钟级别规则，s：秒级规则
warn.rule.type = s

#--------------waverecord.to.mysql配置---------------#
#ftp配置
ftp.host = 172.17.92.181
ftp.port = 21
ftp.username = ftpuag
ftp.pwd = ftpuag

waverecord.application.id = wave-data
waverecord.kafka.source.topics = wave-record-topic
waverecord.kafka.sink.topic = secwarndata-topic
logging.file = logs/record.log

#--------------event.to.mysql配置---------------#
event2mysql.application.id = event2mysqlTest
event2mysql.kafka.source.topics = secwarndata-topic,switchdata-topic,othereventdata-topic

#================================ MyBatis =====================================
mybatis.config.path = mybatis-config.xml
mysql.ds = ds_master,ds_slave
#================================ MySQL =====================================
# db master
mysql.master.url = jdbc:mysql://192.168.1.212:3306/iot_config?useUnicode=true&characterEncoding=utf8&autoReconnect=true&autoReconnectForPools=true
# db slav
mysql.slave.url = jdbc:mysql://192.168.1.212:3306/iot_config?useUnicode=true&characterEncoding=utf8&autoReconnect=true&autoReconnectForPools=true

#--------------alarmerconf配置---------------#
# 是否需要启动时加载档案信息，默认是true
alarmer.starting.load.business = true
alarmer.starting.load.whitelist = true

alarmer.kafka.source.topics = switchdata-topic,othereventdata-topic,secwarndata-topic
alarmer.kafka.consume.poll = 300
# group id
alarmer.kafka.application.name = alarmer
# 要写入的topic
alarmer.kafka.sink.topic = alarmdata-topic

alarmer.envirType = IOE
mysql.url = jdbc:mysql://192.168.1.212:3306/us_app?useSSL=false&useUnicode=true&characterEncoding=UTF-8
mysql.user = root
mysql.password = zhbrpyd
business.telemetry.sql = SELECT  lvb.CJDH TAG_ID, lvb.gjgzmc RULE_NAME, lvb.glsb PATTERN_DEVICE, lvb.xhmc SIG_NAME, lvb.ssxgjjb LIM_MAX_LEVEL, lvb.ssxcxsj LIM_MAX_TIMERANGE, lvb.sxgjjb LIM_UPPER_LEVEL, lvb.sxcxsj LIM_UPPER_TIMERANGE, lvb.xxgjjb LIM_LOW_LEVEL, lvb.xxcxsj LIM_LOW_TIMERANGE, lvb.xxxgjjb LIM_MIN_LEVEL, lvb.xxxcxsj LIM_MIN_TIMERANGE, lvb.LW_RTU_NAME MONITOR_DEVICE_NAME, lvb.guid MONITOR_DEVICE_ID, lvb.stationcode STATION_CODE, lvb.ywdw SERVICE_PROVIDER, tvs.BDZMC STATION_NAME, dept.FULL_NAME SERVICE_NAME, tvs.zcdw ENTERPRISE_ID, (SELECT de.full_name FROM us_sys.tb_sys_department de WHERE de.guid = tvs.zcdw) ENTERPRISE_NAME FROM us_app.tv_station tvs, (SELECT a.CJDH, a.gjgzmc, a.glsb, a.xhmc, a.ssxgjjb, a.ssxcxsj, a.sxgjjb, a.sxcxsj, a.xxgjjb, a.xxcxsj, a.xxxgjjb, a.xxxcxsj, b.LW_RTU_NAME, b.guid, b.stationcode, b.ywdw FROM us_app.tb_fes_ycgjpz a, us_app.fes_lv_term_info b WHERE a.cdmcid = b.guid)lvb, us_sys.tb_sys_department dept WHERE lvb.stationcode = tvs.sbbm AND tvs.YWDW = dept.GUID;
business.telecommunicating.sql = SELECT lvb.CJDH TAG_ID, lvb.GJMS `DESC`, lvb.GLSB PATTERN_DEVICE, lvb.GJJB ALARM_LEVEL, lvb.XHMC SIG_NAME, lvb.LW_RTU_NAME MONITOR_DEVICE_NAME, lvb.guid MONITOR_DEVICE_ID, lvb.stationcode STATION_CODE, lvb.ywdw SERVICE_PROVIDER, tvs.BDZMC STATION_NAME, dept.FULL_NAME SERVICE_NAME FROM us_app.tv_station tvs, (SELECT a.CJDH, a.GJMS, a.GLSB, a.GJJB, a.XHMC, b.LW_RTU_NAME, b.guid, b.stationcode, b.ywdw FROM us_app.tb_fes_yxgjpz a, us_app.fes_lv_term_info b WHERE a.zdmcid = b.guid)lvb, us_sys.tb_sys_department dept WHERE lvb.stationcode = tvs.sbbm AND tvs.YWDW = dept.GUID;


#--------------cache---------------#
#business.jdbc.driver.name=
business.jdbc.password = zhbrpyd
business.jdbc.user = root
business.jdbc.url = jdbc:mysql://192.168.1.212:3306/us_app?useSSL=false&useUnicode=true&characterEncoding=UTF-8

spring.application.name = iot-service
server.port = 8899


eureka.client.registry-fetch-interval-seconds = 5

# 是否使用本地配置文件
spring.profiles.active = native

#--------------kafka2db---------------#
# kafka相关配置
kafka2db.application.id = kafka2tsdb-test
kafka2db.source.topics = seconddata-topic

# 写入InfluxDB

# InfluxDB相关配置=====================================
influxdb.url = http://192.168.1.209:8086
influxdb.dbname = pyd
# influxdb-pool的配置 -------------------------
#池中保留的最多连接总数量
influxdb.pool.max.total = 100
#池中保留的最多空闲连接数量
influxdb.pool.max.idle = 30
#池中保留的最少空闲连接数量
influxdb.pool.min.idle = 20
#获取连接的等待时间
influxdb.pool.max.wait.millis = 3000

kafka2db.num.stream.threads = 2



#=====================公共部分======================
mysql.slave.username = root
mysql.slave.password = zhbrpyd
mysql.master.username = root
mysql.master.password = zhbrpyd

~~~



~~~properties
kafka.bootstrap.servers = M1:9092,M2:9093,S1:9094

#--------------kafka2db---------------#
# kafka相关配置
kafka2db.application.id = kafka2tsdb-test
kafka2db.source.topics = seconddata-topic


#================================ Redis =====================================
redis.common.host = 192.168.1.212
redis.common.port = 6379
redis.common.password = sys
redis.common.database = 5
redis.common.timeout = 2000
redis.common.maxTotal = 200
redis.common.maxWaitMillis = 15000
redis.common.testOnBorrow = true
redis.common.maxIdle = 100

# 写入InfluxDB

# InfluxDB相关配置=====================================
influxdb.url = http://192.168.1.209:8086
influxdb.dbname = pyd
# influxdb-pool的配置 -------------------------
#池中保留的最多连接总数量
influxdb.pool.max.total = 100
#池中保留的最多空闲连接数量
influxdb.pool.max.idle = 30
#池中保留的最少空闲连接数量
influxdb.pool.min.idle = 20
#获取连接的等待时间
influxdb.pool.max.wait.millis = 3000

kafka2db.num.stream.threads = 2
server.port = 8989

~~~



