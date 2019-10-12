# Shell

首先shell挺有意思的，其次，挺有用的。

## 语法

~~~shell
$1 # 获取脚本的第一个参数



~~~





## 群起zookeeper

~~~shell
#!/bin/bash
case $1 in
"start"){
   for i in hadoop104 hadoop105 hadoop106
   do
  		 echo "----------启动$i zk----------"
   		 ssh $i "/opt/module/zookeeper-3.4.10/bin/zkServer.sh start"
   done
};;
"stop"){
   for i in hadoop104 hadoop105 hadoop106
   do
  	        echo "----------关闭$i zk----------"
   	       	ssh $i "/opt/module/zookeeper-3.4.10/bin/zkServer.sh stop"
   done
};;
"status"){
   for i in hadoop104 hadoop105 hadoop106
   do
        	 echo "----------查看$i zk----------"
      		ssh $i "/opt/module/zookeeper-3.4.10/bin/zkServer.sh status"
   done
};;
esac
~~~

##  同步脚本

~~~shell
#!/bin/bash
#1 获取输入参数个数，如果没有参数，直接退出
pcount=$#
if((pcount==0)); then
echo no args;
exit;
fi

#2 获取文件名称
p1=$1
fname=`basename $p1`
echo fname=$fname

#3 获取上级目录到绝对路径
pdir=`cd -P $(dirname $p1); pwd`
echo pdir=$pdir

#4 获取当前用户名称
user=`whoami`

#5 循环
for((host=104; host<107; host++)); do
        echo ------------------- hadoop$host --------------
        rsync -rvl $pdir/$fname $user@hadoop$host:$pdir
done
~~~

## 群发指令

~~~shell
#! /bin/bash

for i in hadoop104 hadoop105 hadoop106
do
        echo --------- $i ----------
        ssh $i "$*"
done
~~~



~~~java 
 private String guid;

    /* 企业用户中文名 */
    private String qyyh;

    /* 企业用户GUID */
    private String qyyhid;

    /* 站房中文名称 */
    private String zfmc;

    /* 站房名称GUID */
    private String zfmcid;

    /* 监测点（采集设备）名称（中文） */
    private String cdmc;

    /* 监测点（采集设备）GUID */
    private String cdmcid;

    /* 信号名称（数据项名称） */
    private String xhmc;

    /* 告警分级，从档案获取，告警级别编码 */
    private String gjjb;

    /* 告警时间 */
    private Date gjsj;

    /* 所属服务商（中文名称） */
    private String ssfws;

    /* 所属服务商GUID */
    private String ssfwsid;

    /* 采集点号，24位字符的数据项编码。 */
    private String cjdh;

    /* 告警描述（用于遥信） */
    private String gjms;

    /* 下面几个字段是在推送使用的 */

    /* 隆基泰和主框架的大类 */
    private String EVT_CLASS;

    /* 隆基泰和主框架的小类 */
    private String EVT_SUBCLASS;

    /* 告警数据项的值 */
    private Double value;
~~~



























