#### orleaapaaccumu
#####1 accumulo data model:
Key (rowid column, timestamp)  
value
How to sort. First sort by id asc, then timestamp desc  
column (family, qualifier(content of column),visibility

Ex: Auth token(A) -->visibility (A|C) ->can see  
Auth token(A) -->visibility (B) ->can not see

#####2
######1 install
install hadoop
```
wget http://apache.claz.org/hadoop/common/hadoop-2.7.2/hadoop-2.7.2.tar.gz
tar zxvf hadoop-2.7.2.tar.gz
mv hadoop-2.7.2 /usr/local/hadoop 
```

then .bashrc
```
export JAVA_HOME=/usr
export HADOOP_PREFIX=/usr/local/hadoop   #for accumulo
export HADOOP_HOME=/usr/local/hadoop
export PATH=$PATH:$HADOOP_HOME/bin
export PATH=$PATH:$HADOOP_HOME/sbin
export HADOOP_MAPRED_HOME=$HADOOP_HOME
export HADOOP_COMMON_HOME=$HADOOP_HOME
export HADOOP_HDFS_HOME=$HADOOP_HOME
export YARN_HOME=$HADOOP_HOME
export HADOOP_COMMON_LIB_NATIVE_DIR=$HADOOP_HOME/lib/native
export HADOOP_OPTS="-Djava.library.path=$HADOOP_HOME/lib"
```
install accumulo
```
wget http://apache.spinellicreations.com/accumulo/1.7.2/accumulo-1.7.2-bin.tar.gz
tar zxvf accumulo-1.7.2-bin.tar.gz
```
then
```
mkdir -p /usr/local/hadoop_tmp/hdfs/namenode && mkdir -p /usr/local/hadoop_tmp/hdfs/datanode
```
open core-site
```
vim /usr/local/hadoop/etc/hadoop/core-site.xml
```
edit
```
<configuration>
<property>
<name>fs.default.name</name>
<value>hdfs://localhost:9000</value>
</property>
</configuration>
```

create accumulo folder:
```
sudo su hduser
hadoop fs -mkdir /accumulo
hadoop fs -chown root /accumulo
hadoop fs -rm -r -f /accumulo
```
if locked,
```
hdfs dfsadmin -safemode leave
```


vim conf/accumulo-env.sh
```
set
```
test -z "$JAVA_HOME" && export JAVA_HOME=/usr/lib/java
test -z "$ZOOKEEPER_HOME" && export JAVA_HOME=/usr/lib/zookeeper
```
Then
```
vim conf/accumulo-site.xml
```
edit
```
property->value>hdfs://train:9000/accumulo
(zookeeper) train:2181
```
generate ssh key:
```
ssh-keygen
```
copy to `localmachine`
```
ubuntu@-22:/home/accumulo-1.7.1/conf$ cat ~/.ssh/id_rsa.pub > ~/.ssh/authorized_keys
```

connect
```
ssh localhost
```

config:
```
vim slaves
vim masters
```
keep default setting.

######using the shell
```
accumulo init
```
using the shell
```
accumulo shell -u root
```
cmds:
```
tables,table
```
others:
```
createuser name
userpermissions -u name
grant System.CREATE_TABLE -s -u name
user name //switch user
```
```
insert row colfamily colquanlifier valuename
scan
```

config:
```
config -f gc  //config gatbage collector
config -t test
```
config table
```
config -t test -s table.bloom.enabled=true
config -t test -f table.bloom.enabled
```
