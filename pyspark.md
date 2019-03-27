# pyspark

# spark访问mongo
  1. 下载 mongo-java-driver-3.6.3.jar		mongo-spark-connector_2.11-2.2.1.jar
  2. spark-defaults.conf中加入：
  ```
 spark.driver.extraClassPath /Users/yinhang/dev/tools/mongo-spark-connector_2.11-2.2.1.jar:/Users/yinhang/dev/tools/mongo-java-driver-3.6.3.jar
 spark.executor.extraClassPath /Users/yinhang/dev/tools/mongo-spark-connector_2.11-2.2.1.jar:/Users/yinhang/dev/tools/mongo-java-driver-3.6.3.jar
 spark.driver.extraLibraryPath /Users/yinhang/dev/tools/mongo-spark-connector_2.11-2.2.1.jar:/Users/yinhang/dev/tools/mongo-java-driver-3.6.3.jar
 spark.executor.extraLibraryPath /Users/yinhang/dev/tools/mongo-spark-connector_2.11-2.2.1.jar:/Users/yinhang/dev/tools/mongo-java-driver-3.6.3.jar
  ```

# macOS安装PySpark

<!--   版本必须对应！ -->
<!-- ``` -->
<!-- export SPARK_HOME=/Users/yinhang/dev/tools/spark-2.3.0-bin-hadoop2.7 -->
<!-- export PATH=$SPARK_HOME/bin:$PATH -->

<!-- export PROTOC_HOME=/Users/yinhang/dev/tools/protobuf -->
<!-- export PATH=$PROTOC_HOME/bin:$PATH -->
<!-- export DYLD_LIBRARY_PATH=/Users/yinhang/dev/tools/protobuf/lib -->

<!-- export HADOOP_HOME=/Users/yinhang/dev/tools/hadoop-3.1.0 -->
<!-- export HADOOP_OPTS="-Djava.library.path=${HADOOP_HOME}/lib/native" -->
<!-- export PATH=$HADOOP_HOME/bin:$PATH -->
<!-- export LD_LIBRARY_PATH=$HADOOP_HOME/lib/native:$LD_LIBRARY_PATH -->
<!-- export JAVA_LIBRARY_PATH=$JAVA_LIBRARY_PATH:${HADOOP_HOME}/lib/native -->
<!-- ``` -->

<!-- 1. tar -xzvf spark-2.3.0-bin-hadoop2.7.tgz -->
<!--    1. 加入SPARK环境变量 -->
<!-- 2. tar -xzvf protobuf-2.5.0.tar.gz -->
<!--    1. /configure --prefix=/Users/yinhang/dev/tools/protobuf      -->
<!--    2. make -j4  -->
<!--    3. make install -->
<!--    4. 加入protol buffer环境变量 -->
<!-- 3. tar -xzvf hadoop-3.1.0-src.tar.gz -->
<!--    1. export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk1.8.0_152.jdk/Contents/Home -->
<!--    2. tar -xzvf apache-maven-3.5.3-bin.tar.gz -->
<!--    3. ../apache-maven-3.5.3/bin/mvn package -Pdist,native -DskipTests -Dtar -Dmaven.javadoc.skip=true -->
<!--    4. cp -r hadoop-dist/target/hadoop-3.1.0 ~/dev/tools/ -->
<!--    5. 加入HADOOP环境变量 -->
<!-- 4. pip install findspark -->

1. brew install apache-spark
2. cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
3. ssh localhost
4. cd /usr/local/Cellar/hadoop
5. mkdir -p tmp/dfs/data
6. cd 3.1.1
7. vi libexec/etc/hadoop/core-site.xml
   ```xml
<configuration>
  <property>
    <name>fs.defaultFS</name>
    <value>hdfs://localhost:9000</value>
  </property>
  <property>
    <name>hadoop.tmp.dir</name>
    <value>file:/usr/local/Cellar/hadoop/tmp</value>
  </property>
</configuration>
   ```
8. vi libexec/etc/hadoop/hdfs-site.xml
  ```xml
<configuration>
  <property>
    <name>dfs.replication</name>
    <value>1</value>
  </property>
  <property>
    <name>dfs.permissions</name>
    <value>false</value>
  </property>
  <property>
    <name>dfs.namenode.name.dir</name>
    <value>file:/usr/local/Cellar/hadoop/tmp/dfs/name</value>
  </property>
  <property>
    <name>dfs.datanode.data.dir</name>
    <value>file:/usr/local/Cellar/hadoop/tmp/dfs/data</value>
  </property>
</configuration>  
  ```
9. vi libexec/etc/hadoop/mapred-site.xml
  ```xml
<configuration>
  <property>
    <name>mapreduce.framework.name</name>
    <value>yarn</value>
  </property>
  <property>
    <name>mapred.job.tracker</name>
    <value>localhost:9010</value>
  </property>
  <property>
    <name>yarn.app.mapreduce.am.env</name>
    <value>HADOOP_MAPRED_HOME=/usr/local/Cellar/hadoop/3.1.1/libexec</value>
  </property>
  <property>
    <name>mapreduce.map.env</name>
    <value>HADOOP_MAPRED_HOME=/usr/local/Cellar/hadoop/3.1.1/libexec</value>
  </property>
  <property>
    <name>mapreduce.reduce.env</name>
    <value>HADOOP_MAPRED_HOME=/usr/local/Cellar/hadoop/3.1.1/libexec</value>
  </property>
</configuration>

  ```
10. libexec/etc/hadoop/yarn-site.xml
  ```xml
<configuration>
  <property>
    <name>yarn.nodemanager.aux-services</name>
    <value>mapreduce_shuffle</value>
  </property>
  <property>
    <name>yarn.nodemanager.env-whitelist</name>
    <value>JAVA_HOME,HADOOP_COMMON_HOME,HADOOP_HDFS_HOME,HADOOP_CONF_DIR,CLASSPATH_PREPEND_DISTCACHE,HADOOP_YARN_HOME,HADOOP_MAPRED_HOME</value>
  </property>
</configuration>
  ```
11. cd /usr/local/Cellar/hadoop
12. bin/hdfs namenode -format
13. sbin/start-dfs.sh
14. 可打http://localhost:9870
15. sbin/start-yarn.sh
16. 可打http://localhost:8088
17. spark-shell
18. pip install findspark

# 测试安装

```python
import findspark
findspark.init()
import pyspark
from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate()
df = spark.read.csv("sample.csv", inferSchema=True, header=True)

df.columns

df.count()

df.printSchema()

df.show(3)

# 选择列
df.select("age", "mobile").show(5)

df.describe().show()

# 增加列
df.withColumn("new_column", (df["column_name"]+1)).show(10, False)

# 转换数据类型
from pyspark.sql.types import StringType, DoubleType
df.withColumn("new_column", df["column_name"].cast(DoubleType())).show(10)

# 过滤数据
df.filter(df["nnn"]=="vvv")
df.filter(df["nn1"]=="vv1").filter(df["nn2"]=="vv2")
df.filter((df["nn1"]=="vv1")&(df["nn2"]>"vv2"))

# unique
df.select("nn1").distinct()
df.select("nn1").distinct().count()

# group by
df.groupBy("nn1").count().show()

# order by
df.groupBy("nn1").count().orderBy("count", ascending=False).show()

# agg
df.groupBy("nn1").mean().show()
df.groupBy("nn1").sum().show()
df.groupBY("nn1").max().show()
df.groupBy("nn1").min().show()
df.groupBy("nn1").agg({"nn2": "sum"}).show()

# UDF
from pyspark.sql.functions import udf

def func1(arg1):
    ...

f_udf = udf(func1, StringType())
df.withColumn("new_column", f_udf(df["old_column"])).show()



```

# dfs 命令

- 导入文件

  hdfs dfs -copyFromLocal test.csv /usr/test
  
  
