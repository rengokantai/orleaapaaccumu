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
```
wget ....
tar ....
vi conf/accumulo-env.sh
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
