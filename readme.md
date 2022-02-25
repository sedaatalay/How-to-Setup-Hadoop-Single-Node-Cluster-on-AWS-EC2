# Satalay

# Setting up Hadoop to AWS EC2 and running a sample mapreduce
### 1- Login to AWS and launch an instance
![1.png](attachment:32ee3602-293b-47a1-b75b-ec80007a47b2.png)

### 2- Select Ubuntu Server 18.04 LTS
![2.png](attachment:2191e541-6bbc-4fcc-8315-5fd76f487786.png)

### 3- Choose an Instance Type (Choose recommended)
![3.png](attachment:61e0377c-3ad9-45b2-a89e-cef900a81201.png)

### 4- The instance Auto-assing Public IP has to be enable
![4.png](attachment:45920560-5957-452e-a5ce-23b27bbc14a6.png)

### 5- For larger size installations we can add additional volume
![5.png](attachment:fb4add6d-ad19-430d-b20b-43a80289abf1.png)

### 6- Make sure the security group type has all traffic allowed to inbound and outbound that you need
![6.png](attachment:a00a0a26-1996-48c7-9c5f-2e837a72f33d.png)

### 7- Create a Private Key file (.pem)
![Ekran Resmi 2022-02-25 01.07.46.png](attachment:1e2790b9-3d15-48a1-b710-3cf6a9d5b7b5.png)

### 8- Launch the Instance
![8.png](attachment:14d00b9b-75d6-4970-a0af-3c52df9696fd.png)

### 9- Assign Elastic IP to Instance
![Ekran Resmi 2022-02-25 01.09.42.png](attachment:eb1fac53-6e43-40ff-aa2d-1f0e065c908f.png)

### 10- Associate the elastic IP to the Instance
![Ekran Resmi 2022-02-25 01.11.38.png](attachment:589ccc2c-f296-468d-aed6-51387fea9c83.png)
![Ekran Resmi 2022-02-25 01.11.47.png](attachment:e54768b2-a1c3-45cb-9c17-74b55115a521.png)
![Ekran Resmi 2022-02-25 01.12.17.png](attachment:bc674e49-6dd3-4153-a5d1-344d8d486b54.png)

### 11- Change the permission of Private Key
```console
chmod 400 <pem file name>.pem
```
![Ekran Resmi 2022-02-25 01.32.26.png](attachment:3580fb2c-5545-4d99-9e52-0ab546e0d187.png)

### 12- Connect using SSH
```console
ssh -i <pem file name> ubuntu@public-dns-name
```
![Ekran Resmi 2022-02-25 01.32.26.png](attachment:3580fb2c-5545-4d99-9e52-0ab546e0d187.png)

### 13- Update the packages
```console
sudo apt update
sudo apt upgrade
```
![Ekran Resmi 2022-02-25 01.34.10.png](attachment:174aace2-c4f6-41f9-900a-9210bde28171.png)

### 14- Change Hostname to hadoop
```console
sudo nano /etc/hostname
```
![Ekran Resmi 2022-02-25 01.37.49.png](attachment:7582999e-f9d0-479b-ba03-6348eaa3686b.png)

### 15- Reboot and then Reconnect to Instance
```console
sudo reboot
```
![Ekran Resmi 2022-02-25 01.39.39.png](attachment:6dc10d0f-12a0-44a8-bb09-57dd23e9a821.png)

```console
ssh -i <pem file name> ubuntu@public-dns-name
```
![Ekran Resmi 2022-02-25 01.40.10.png](attachment:8a2c9272-ae94-4783-a966-c4f1a7f1e04a.png)

### 16- Install Open JDK 8 
```console
sudo apt install openjdk-8-jdk
```
![Ekran Resmi 2022-02-25 01.40.34.png](attachment:ceca3a70-6941-4aa4-a929-1fa7f8428cc1.png)

### 17- Download and Install Hadoop
#### Go to Hadoop -> Downloads page

![23.png](attachment:862eff52-1bd8-4bb0-9697-af716de1af26.png)
![24.png](attachment:ea502ad9-a3b4-4e6c-824e-444518cc461e.png)

#### Install and extract the package
```console
wget <link> -P ~/Downloads
sudo tar zxvf ~/Downloads/hadoop-* -C /usr/local
```
![Ekran Resmi 2022-02-25 01.42.38.png](attachment:dc1cf4f5-1188-4350-aef1-36ed3a6dae10.png)

### 18- Rename the folder
```console
sudo mv /usr/local/hadoop-* /usr/local/hadoop
```
![Ekran Resmi 2022-02-25 01.44.25.png](attachment:a0c72d4d-cae7-4e9a-b939-555b471bd7bc.png)

### 19- Setting up of Environment
#### Open .bashrc file
```console
nano ~/.bashrc
```
##### Write into
```console
export HADOOP_HOME=/usr/local/hadoop
export HADOOP_INSTALL=$HADOOP_HOME
export HADOOP_MAPRED_HOME=$HADOOP_HOME
export HADOOP_COMMON_HOME=$HADOOP_HOME
export HADOOP_CONF_DIR=/usr/local/hadoop/etc/hadoop
export HADOOP_HDFS_HOME=$HADOOP_HOME
export YARN_HOME=$HADOOP_HOME
export HADOOP_COMMON_LIB_NATIVE_DIR=$HADOOP_HOME/lib/native
export PATH=$PATH:$HADOOP_HOME/sbin:$HADOOP_HOME/bin
$
```
![Ekran Resmi 2022-02-25 01.44.56.png](attachment:d07428b9-e69d-4dd3-b459-aa6d9ea19be9.png)

#### For reflecting to current session
```console
source ~/.bashrc
```
![Ekran Resmi 2022-02-25 01.46.52.png](attachment:5b90ab7a-9806-48c8-b54f-079c4ceb4d87.png)

#### Open hadoop-env.sh from $HADOOP_CONF_DIR
$
```console
sudo nano $HADOOP_CONF_DIR/hadoop-env.sh
$
```
![Ekran Resmi 2022-02-25 01.53.17.png](attachment:d60b8d5d-32d6-486d-8a80-6494cba86a9f.png)
![Ekran Resmi 2022-02-25 01.50.01.png](attachment:e8120b79-306c-4369-9f1e-cbafe7698cbf.png)

##### Change Java Home and Hadoop Conf Dir as below
```console
export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
export HADOOP_CONF_DIR=/usr/local/hadoop/etc/hadoop
```
![Ekran Resmi 2022-02-25 01.51.23.png](attachment:30f59097-eeef-4fc0-a8dc-4152280e5918.png)

### 20- SSH Connection
#### Upload <your_key_pair> file to .ssh directory (Open your local (not instance) and upload .pem from local to instance)
```console
scp -i <Path of .pem> <pem file name> ubuntu@<your_elastic_ip>:/home/ubuntu
```
#### Reconnect to instance and check .pem file load control
```console
ssh -i <pem file name> ubuntu@public-dns-name
ls
```
#### Copy <your_key_pair> to instance
```console
cp <pem file name> ~/.ssh/
```
##### For Windows:
##### Locate .ssh directory and perform the same

![Ekran Resmi 2022-02-25 02.02.11.png](attachment:8fa3c2e0-b260-483e-9b4d-6e00945879d7.png)

#### Create a config file in .ssh directory of local system (not Instance)
```console
nano ~/.ssh/config
```
##### Write into
```console
Host hadoop
  HostName <publicDnsname>
  User ubuntu
  IdentityFile ~/.ssh/<pem file name>
```
![Ekran Resmi 2022-02-25 02.04.54.png](attachment:38c69ccc-d31f-4d85-94e1-edc4f23f6302.png)

![Ekran Resmi 2022-02-25 02.07.50.png](attachment:0686191b-217c-4f55-be0c-2fee5ca12482.png)

#### Copy the config and pem files to Instance .ssh directory
```console
scp ~/.ssh/config hadoop:~/.ssh
$ scp ~/.ssh/*.pem hadoop:~/.ssh
$
```
![Ekran Resmi 2022-02-25 02.11.45.png](attachment:3535d330-9035-4af4-8ede-a7d86e434f34.png)

#### Reconnect to instance and create public key
```console
ssh -i <pem file name> ubuntu@public-dns-name
ssh hadoop
ssh-keygen -f ~/.ssh/id_rsa -t rsa -P ""
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
```
![Ekran Resmi 2022-02-25 02.14.49.png](attachment:d583fa1c-db16-4934-940c-b5360b24e6cd.png)

![Ekran Resmi 2022-02-25 02.15.13.png](attachment:88461c8e-0859-4639-b2d8-bfc4d3dfa6c9.png)

#### Open /etc/hosts and add instance IPV4 address with hostname 
```console
sudo nano /etc/hosts
```
![Ekran Resmi 2022-02-25 02.17.08.png](attachment:1ae075b3-d42a-4fd6-8940-2828c95a84ca.png)


### 21- Hadoop Configuration
#### Edit core-site.xml
```console
sudo nano $HADOOP_CONF_DIR/core-site.xml
$
```
##### Write into
```console
<configuration>
  <property>
    <name>fs.defaultFS</name>
    <value>hdfs://<your public dns name>:9000</value>
  </property>
</configuration>
```
![Ekran Resmi 2022-02-25 02.19.29.png](attachment:08f74657-91ce-4aef-94b0-6eff38d064d9.png)

#### Edit yarn-site.xml
```console
sudo nano $HADOOP_CONF_DIR/yarn-site.xml
$
```
##### Write into
```console
<configuration>
  <property>
    <name>yarn.nodemanager.aux-services</name>
    <value>mapreduce_shuffle</value>
  </property>
  <property>
    <name>yarn.resourcemanager.hostname</name>
    <value><your public dns name></value>
  </property>
</configuration>
```
![Ekran Resmi 2022-02-25 02.20.40.png](attachment:9f4fb3db-ddc9-4541-a5db-bb8e9cbfe1b8.png)


#### Edit mapred-site.xml from mapred-site.xml.template
```console
sudo cp $HADOOP_CONF_DIR/mapred-site.xml.template $HADOOP_CONF_DIR/mapred-site.xml
```
##### Write into
```console
<configuration>
  <property>
    <name>mapreduce.jobtracker.address</name>
    <value><your public dns name>:54311</value>
  </property>
  <property>
    <name>mapreduce.framework.name</name>
    <value>yarn</value>
  </property>
</configuration>
```
![Ekran Resmi 2022-02-25 02.21.57.png](attachment:cf609401-f4b4-448e-bcdb-6a760aba3475.png)

#### Edit hdfs-site.xml
```console
sudo nano $HADOOP_CONF_DIR/hdfs-site.xml
$
```
##### Write into
```console
<configuration>
  <property>
    <name>dfs.replication</name>
    <value>1</value>
  </property>
  <property>
    <name>dfs.namenode.name.dir</name>
    <value>file:///usr/local/hadoop/data/hdfs/namenode</value>
  </property>
  <property>
    <name>dfs.datanode.data.dir</name>
    <value>file:///usr/local/hadoop/data/hdfs/datanode</value>
  </property>
</configuration>
```
![Ekran Resmi 2022-02-25 02.22.40.png](attachment:d50dc8ca-4091-4c99-8f20-f45ad65c3595.png)

![Ekran Resmi 2022-02-25 02.23.02.png](attachment:cd86a749-ea5d-4e00-8c33-7b711e6ca490.png)


#### Make namenode and datanode directories
```console
sudo mkdir -p $HADOOP_HOME/data/hdfs/namenode
sudo mkdir -p $HADOOP_HOME/data/hdfs/datanode
```
#### Change the owner 
```console
sudo chown -R ubuntu $HADOOP_HOME
$
```
#### Change masters and slaves to hadoop
```console
sudo nano $HADOOP_HOME/masters
sudo nano $HADOOP_HOME/slaves
```
![Ekran Resmi 2022-02-25 02.23.43.png](attachment:4ad4e748-9508-40fb-b2bc-09a85d9b14bc.png)
![Ekran Resmi 2022-02-25 02.24.04.png](attachment:a6e1b126-085f-46c2-9e27-4e076a23db2b.png)
![Ekran Resmi 2022-02-25 02.24.24.png](attachment:c84752cc-33f6-49b7-baa7-08fb0689d3c6.png)


### Launch Hadoop Cluster 
#### Format and start hdfs
```console
hdfs namenode -format
$HADOOP_HOME/sbin/start-dfs.sh
$ 
```
![Ekran Resmi 2022-02-25 02.58.10.png](attachment:6e3c99b3-57df-48a8-834f-1a538c552279.png)

#### Start yarn
```console
$HADOOP_HOME/sbin/start-yarn.sh
$
```
![Ekran Resmi 2022-02-25 02.59.40.png](attachment:11cdbbe0-0b37-4fc7-a4a5-b9e665626b1f.png)

#### Start the job history server
```console
$HADOOP_HOME/sbin/mr-jobhistory-daemon.sh start historyserver
$
```
#### To see the Java processes
```console
jps
```
![Ekran Resmi 2022-02-25 03.00.06.png](attachment:53266425-a5be-4073-80d4-bbb5cb127be5.png)


### Accessing NameNode using WebUI
#### Namenode Overview
```console
publicdns:50070
```
![Ekran Resmi 2022-02-25 03.01.17.png](attachment:f9ce93a0-6b6e-448f-8294-e31e866c7b90.png)

#### Cluster Metrics Overview
```console
publicdns:8088
```
![Ekran Resmi 2022-02-25 03.01.36.png](attachment:651e31e5-3ed7-4b65-9c78-c933f06bf9d2.png)




# Running a sample mapreduce
### Creating an input file
```console
nano input
```
![Ekran Resmi 2022-02-25 03.04.03.png](attachment:87e50682-e4b6-4373-bb17-0ddc687fc8ce.png)

### Creating a Directory in HDFS and Copying file from Local to HDFS
```console
hdfs dfs -mkdir -p WordCount/input
hdfs dfs -put input WordCount/input
```
### Running MapReduce
```console
hadoop jar $HADOOP_HOME/share/hadoop/mapreduce/hadoop-mapreduce-examples-2.8.5.jar wordcount WordCount/input WordCount/output
$
```
![Ekran Resmi 2022-02-25 03.05.19.png](attachment:7690cb3d-0ab0-4b00-b2b4-413ae0a8bf37.png)

### Output
```console
hdfs dfs -cat WordCount/output/part-r-00000
```
![Ekran Resmi 2022-02-25 03.05.28.png](attachment:d7b7bee7-2dbb-4322-9ecb-7737531a82f6.png)


# Before logout, make sure to stop Hadoop services and AWS Instance
```console
$HADOOP_HOME/sbin/mr-jobhistory-daemon.sh stop historyserver
$HADOOP_HOME/sbin/stop-all.sh
```
![Ekran Resmi 2022-02-25 03.06.39.png](attachment:9829409c-2875-442b-b61e-b979971e04cf.png)



## Seda Atalay

