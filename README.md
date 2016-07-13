# RHive-vagrant
My RHive dev system install scripts


# Installed
* Apache Hadoop 2.7.2
* Apache Hive 2.1.0
* Apache Ant 1.9.7
* Openjdk-8-jdk
* R 3.3.1(latest)


# Running Steps
## 0. Cloning Git Repository
```
$ git clone https://github.com/Vazrupe/RHive-vagrant
$ cd RHive-vagrant
```


## 1. Vagrant Build
```
RHive-vagrant$ vagrant up --provider virtualbox && vagrant ssh
```

### Machine Option
* RAM 1G
* Private IP 192.168.33.10
* Host hadoop


## 2. Default Setting
```
hadoop:~$ sudo /scripts/default.sh
```

### System Setting
| Settings | Set |
| -------- | --- |
| Timezone | Asia/Seoul |
| Language | ko_KR.UTF_8 |
| Swap Memory | 2G |
| Java | openjdk-8-jdk |
| R | 3.3.1 (latest) |
| Ant | 1.9.7 |

## 3. Hadoop, Hive Install
```
hadoop:~$ /scripts/install-Hadoop.sh; source ~/.bashrc
```
### Hadoop Setting
| File | Name | Value |
| ---- | ---- | ----- |
| hadoop-env.sh | JAVA_HOME | /usr/lib/jvm/java-8-openjdk-amd64 |
| hadoop-env.sh | HADOOP_HOME | /home/vagrant/hadoop-2.7.2 |
| hadoop-env.sh | HADOOP_PREFIX | $HADOOP_HOME |
| hadoop-env.sh | HADOOP_INSTALL | $HADOOP_HOME |
| hadoop-env.sh | HADOOP_CONF_DIR | $HADOOP_HOME/etc/hadoop |
| hadoop-env.sh | YARN_HOME | $HADOOP_HOME |
| hadoop-env.sh | YARN_CONF_DIR | $YARN_HOME/etc/hadoop |
| core-site.xml | fs.default.name | hdfs://0.0.0.0:19000 |
| core-site.xml | hadoop.proxyuser.vagrant.hosts | * |
| core-site.xml | hadoop.proxyuser.vagrant.groups | * |
| hdfs-site.xml | dfs.replication | 1 |
| hdfs-site.xml | dfs.namenode.datanode.registration.ip-hostname-check | false |
| hdfs-site.xml | dfs.namenode.name.dir | /home/vagrant/hadoop-2.7.2/dfs/name |
| hdfs-site.xml | dfs.datanode.data.dir | /home/vagrant/hadoop-2.7.2/dfs/name |
| mapred-site.xml | mapred.job.tracker | 0.0.0.0:54311 |

### Hive Setting
| File | Name | Value |
| ---- | ---- | ----- |
| hive-env.sh | HADOOP_HOME | /home/vagrant/hadoop-2.7.2 |

## 4. RHive Install
```
hadoop:~$ sudo -E /scripts/install-RHive.sh
```


## 5. Running Hadoop
```
hadoop:~$ hadoop namenode -format; $HADOOP_HOME/sbin/start-all.sh
hadoop:~$ jps
xxxx DataNode
xxxx ResourceManager
xxxx SecondaryNameNode
xxxx NodeManager
xxxx Jps
xxxx NameNode
```


## 6. Running Hive
```
hadoop:~$ cd $HIVE_HOME
hadoop:{$HIVE_HOME}$ hive --service hiveserver2 &
hadoop:{$HIVE_HOME}$ netstat -npl | grep :10000
hadoop:{$HIVE_HOME}$ cd ~
```


## 7. Connect RHive
```
hadoop:~$ R
> library(RHive)
> rhive.init()
> rhive.connect('0.0.0.0', 10000, hiveServer2=TRUE)
```



# Requirement
* Oracle VirtualBox
* Vagrant
* ssh / (Windows)putty or other ssh client
