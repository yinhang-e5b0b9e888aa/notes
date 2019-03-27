# hive

## macos 安装

  0. 先要配置hadoop home:
     
     export JAVA_HOME=$(/usr/libexec/java_home)
     export HADOOP_HOME=/usr/local/Cellar/hadoop/3.1.1/libexec
     export PATH=$PATH:$HADOOP_HOME/bin
     
  1. brew install hive mysql
  2. mysql_secure_installation
  3. mysql -uroot -p
  4. 在mysql中执行:
     1). create database metastore;
     2). create user 'hive'@'localhost' identified by '123456';
     3). grant select,insert,update,delete,alter,create,index,references on metastore.* to 'hive'@'localhost';
     4). flush privileges;
  5. cd /usr/local/Cellar/hive/3.1.1/libexec/conf
  6. cp hive-default.xml.template hive-site.xml
  7. vi hive_site.xml 修改如下项
     ```xml
<property>
  <name>javax.jdo.option.ConnectionURL</name>
  <value>jdbc:mysql://localhost/metastore</value>
</property>

<property>
  <name>javax.jdo.option.ConnectionDriverName</name>
  <value>com.mysql.jdbc.Driver</value>
</property>

<property>
  <name>javax.jdo.option.ConnectionUserName</name>
  <value>hive</value>
</property>

<property>
  <name>javax.jdo.option.ConnectionPassword</name>
  <value>123456</value>
</property>

<property>
  <name>hive.exec.local.scratchdir</name>
  <value>/tmp/hive</value>
</property>

<property>
  <name>hive.querylog.location</name>
  <value>/tmp/hive</value>
</property>

<property>
  <name>hive.downloaded.resources.dir</name>
  <value>/tmp/hive</value>
</property>

<property>
  <name>hive.server2.logging.operation.log.location</name>
  <value>/tmp/hive</value>
</property>

     ```
 8. 下载mysql-connector-java
 9. cp mysql-connector-java-8.0.15.jar /usr/local/Cellar/hive/3.1.1/libexec/lib
 10. schematool -initSchema -dbType mysql
 11. hive
 12. 在hive中执行show databases; 无报错
 
## HiveQL 使用

   **HiveQL statements are automatically translated into MapReduce jobs**
   
   Hive不支持对某个具体行的操作，对数据的操作只支持覆盖原数据和追加数据。
   
   Hive也不支持事务和索引。

   https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF

 - 查看函数
 
   ```
   SHOW FUNCTIONS;
   
   DESCRIBE FUNCTION <function_name>;
   
   DESCRIBE FUNCTION EXTENDED <function_name>;
   ```

 - 建表
 
   ```
create external table OnlineRetail (
  InvoiceNo string,
  StockCode string,
  Description string,
  Quantity integer,
  InvoiceDate string,
  UnitPrice float,
  CustomerID string,
  Country string
) ROW FORMAT DELIMITED
FIELDS TERMINATED BY ','
LOCATION '/user/normal';
   ```
   
 - 查询
 
   ```
SELECT COUNT(*) FROM OnlineRetail;

SELECT Description, COUNT(*) as c FROM OnlineRetail GROUP BY Description ORDER BY c DESC;
   ```
   
 - 插入
 
   ```
INSERT INTO TABLE tablename1 select_statement1 FROM from_statement;

WITH tablename1 AS (select_statement1 FROM from_statement) INSERT INTO TABLE tablename2;

   ```

 - 替换
 
   ```
INSERT OVERWRITE TABLE tablename1 select_statement1 FROM from_statement;

WITH tablename1 AS (select_statement1 FROM from_statement) INSERT OVERWRITE TABLE tablename2;
   ```
