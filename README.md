# msyql_client_bench
benchmark for mysql client in python
thon下mysql的客户端主流有三个pymysql, mysqldb 和 mysql connector。很多人在选择客户端时，没有什么要求，都是按照前人或者经验主义选择，但是有真的研究他们之间的性能差别，以及是否符合你的项目需要，或者遇到性能瓶颈时，是否了解他们之间的差别。

本文将从2个维度来分析他们的性能，一个是直接使用，另一个是使用orm辅助使用，来对比三个的性能差别。

介绍
mysql的python客户端目前市场主流有三个，分别是 mysqldb (mysqlclient), mysql connector python 和 pymysql。

mysqldb (mysqlclient) 是mysql官方推出基于C库来写mysql连接库，非纯python。之前mysqldb只支持python2，后面mysqlclient在mysqldb的基础上fork来支持python3。

mysql connector for python 是mysql官方推出的纯python实现的连接库。

pymysql 是纯python写的主流连接库。

环境
host: centos 7.2 4核8G内存
mysql version: 5.6.43
python version: 3.6.6
pymysql: 0.9.3
mysqlclient: 1.4.2.post1
mysql-connector-python: 8.0.15
mysqlalchemy: 1.2.18
测试数据库: mysql 提供的 sakila
测试
查询库表返回 100 条记录

SELECT payment_id,customer_id,staff_id FROM payment where payment_id between 1 and 100 limit 100
非ORM操作
测试方法

重复操作100次

测试结果

connector:0.023178300936706364
pymysql:0.023064655950292945
mysqlclient:0.014133377000689507
测试结论

mysqlclient 效果比其他两个快近100%， 毕竟是依赖c的库，性能是有保障的，connector跟pymysql的就不分上下很接近。

ORM操作
测试方法

重复操作100次

测试结果

connector:0.10195669997483492
pymysql:0.18848947307560593
mysqlclient:0.18876364000607282
测试结论

发现connector比其他两个快将近80%多，其余两个效果也很接近。但是这里会发现使用ORM会整体慢1个数据级。

结论
如果是追求极致性能，建议使用mysqlclient，如果想使用ORM，建议使用mysql connector for python， 后面附带源码。

源码下载

作者：roger_luo
链接：https://www.jianshu.com/p/a1968d0b75e2
来源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
