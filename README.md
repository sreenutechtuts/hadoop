# Hadoop Installation


## Step 1: Install Java 8

sudo apt install openjdk-8-jdk



Once installation is done check the java is installed or not
Execute below command

cd /usr/lib/jvm 
then
ls


## Step 2: Update .bashrc

type cd and enter to come to the root folder

export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64 
export PATH=$PATH:/usr/lib/jvm/java-8-openjdk-amd64/bin 
export HADOOP_HOME=~/hadoop-3.2.4/ 
export PATH=$PATH:$HADOOP_HOME/bin 
export PATH=$PATH:$HADOOP_HOME/sbin 
export HADOOP_MAPRED_HOME=$HADOOP_HOME 
export YARN_HOME=$HADOOP_HOME 
export HADOOP_CONF_DIR=$HADOOP_HOME/etc/hadoop 
export HADOOP_COMMON_LIB_NATIVE_DIR=$HADOOP_HOME/lib/native 
export HADOOP_OPTS="-Djava.library.path=$HADOOP_HOME/lib/native" 
export HADOOP_STREAMING=$HADOOP_HOME/share/hadoop/tools/lib/hadoop-streaming-3.2.4.jar
export HADOOP_LOG_DIR=$HADOOP_HOME/logs 
export PDSH_RCMD_TYPE=ssh

## Step 3: Install ssh

ssh — secure shell — protocol used to securely connect to remote server/system — transfers data in encrypted form

sudo apt-get install ssh

## Step 4: Download apache hadoop

Type apache hadoop in google then go to downloads and download hadoop-3.2.4 binary file

Extract the file 
tar -zxvf ~/Downloads/hadoop-3.2.4.tar.gz

## Step 5: Check hadoop installed or not
cd hadoop-3.2.4
ls /etc/hadoop
it will display hadoop files

## Step 6: Set JAVA_HOME in hadoop-env.sh
sudo nano hadoop-env.h
JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64

## Step 7: update core-site.xml
sudo nano core-site.xml
<configuration> 
 <property> 
 <name>fs.defaultFS</name> 
 <value>hdfs://localhost:9000</value>  </property> 
 <property> 
<name>hadoop.proxyuser.dataflair.groups</name> <value>*</value> 
 </property> 
 <property> 
<name>hadoop.proxyuser.dataflair.hosts</name> <value>*</value> 
 </property> 
 <property> 
<name>hadoop.proxyuser.server.hosts</name> <value>*</value> 
 </property> 
 <property> 
<name>hadoop.proxyuser.server.groups</name> <value>*</value> 
 </property> 
</configuration>

## Step 8: update hdfs-site.xml

sudo nano hdfs-site.xml

<configuration> 
 <property> 
 <name>dfs.replication</name> 
 <value>1</value> 
 </property> 
</configuration>

## Step 9: update mapred-site.xml

sudo nano mapred-site.xml

<configuration> 
 <property> 
 <name>mapreduce.framework.name</name>  <value>yarn</value> 
 </property> 
 <property>
 <name>mapreduce.application.classpath</name> 
  
<value>$HADOOP_MAPRED_HOME/share/hadoop/mapreduce/*:$HADOOP_MAPRED_HOME/share/hadoop/mapreduce/lib/*</value> 
 </property> 
</configuration>


## Step 10: Update yarn-site.xml

sudo nano yarn-site.xml

<configuration> 
 <property> 
 <name>yarn.nodemanager.aux-services</name> 
 <value>mapreduce_shuffle</value> 
 </property> 
 <property> 
 <name>yarn.nodemanager.env-whitelist</name> 
  
<value>JAVA_HOME,HADOOP_COMMON_HOME,HADOOP_HDFS_HOME,HADOOP_CONF_DIR,CLASSPATH_PREP END_DISTCACHE,HADOOP_YARN_HOME,HADOOP_MAPRED_HOME</value> 
 </property> 
</configuration>


## Step 11: Execute below commands for ssh

ssh localhost 
ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa 
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys 


chmod 0600 ~/.ssh/authorized_keys 


hadoop-3.2.4/bin/hdfs namenode -format

format the file system
export PDSH_RCMD_TYPE=ssh

## Step 12: Start hadoop
start-all.sh

## Step 13: open http://localhost:9870

hadoop fs -mkdir /user
hadoop fs mkdire /user/sreenu
touch demo.csv
hadoop fs -put demo.csv /user/sreenu

## Step 14: Stop hadoop 

stop-all.sh



