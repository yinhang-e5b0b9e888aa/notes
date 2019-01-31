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

  版本必须对应！
```
export SPARK_HOME=/Users/yinhang/dev/tools/spark-2.3.0-bin-hadoop2.7
export PATH=$SPARK_HOME/bin:$PATH

export PROTOC_HOME=/Users/yinhang/dev/tools/protobuf
export PATH=$PROTOC_HOME/bin:$PATH
export DYLD_LIBRARY_PATH=/Users/yinhang/dev/tools/protobuf/lib

export HADOOP_HOME=/Users/yinhang/dev/tools/hadoop-3.1.0
export HADOOP_OPTS="-Djava.library.path=${HADOOP_HOME}/lib/native"
export PATH=$HADOOP_HOME/bin:$PATH
export LD_LIBRARY_PATH=$HADOOP_HOME/lib/native:$LD_LIBRARY_PATH
export JAVA_LIBRARY_PATH=$JAVA_LIBRARY_PATH:${HADOOP_HOME}/lib/native
```

1. tar -xzvf spark-2.3.0-bin-hadoop2.7.tgz
   1. 加入SPARK环境变量
2. tar -xzvf protobuf-2.5.0.tar.gz
   1. /configure --prefix=/Users/yinhang/dev/tools/protobuf     
   2. make -j4 
   3. make install
   4. 加入protol buffer环境变量
3. tar -xzvf hadoop-3.1.0-src.tar.gz
   1. export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk1.8.0_152.jdk/Contents/Home
   2. tar -xzvf apache-maven-3.5.3-bin.tar.gz
   3. ../apache-maven-3.5.3/bin/mvn package -Pdist,native -DskipTests -Dtar -Dmaven.javadoc.skip=true
   4. cp -r hadoop-dist/target/hadoop-3.1.0 ~/dev/tools/
   5. 加入HADOOP环境变量
4. pip install findspark
