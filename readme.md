# Setting up Hadoop to AWS EC2 and Running a sample mapreduce

### 1- Login to AWS and launch an instance
<img width="1233" alt="1" src="https://user-images.githubusercontent.com/91700155/155763011-3394af20-a088-40a1-8b7b-947ac74644af.png">

### 2- Select Ubuntu Server 18.04 LTS
<img width="1398" alt="2" src="https://user-images.githubusercontent.com/91700155/155763051-6124c606-d9f2-4128-abae-a0d059d77bf5.png">

### 3- Choose an Instance Type (Choose recommended)
<img width="1425" alt="3" src="https://user-images.githubusercontent.com/91700155/155763077-400b3591-5b55-47a6-a87f-f7b3b4f4ac41.png">

### 4- The instance Auto-assing Public IP has to be enable
<img width="1420" alt="4" src="https://user-images.githubusercontent.com/91700155/155763098-ad4ebc97-3c07-4d58-8bc5-d1609b49f491.png">

### 5- For larger size installations we can add additional volume
<img width="1414" alt="5" src="https://user-images.githubusercontent.com/91700155/155763110-43cf1718-a01a-40f6-86b0-778e8cef6844.png">

### 6- Make sure the security group type has all traffic allowed to inbound and outbound that you need
<img width="1427" alt="6" src="https://user-images.githubusercontent.com/91700155/155763140-77071ba7-b292-4d58-b028-693a6e7c7f87.png">

### 7- Create a Private Key file (.pem)
<img width="1403" alt="Ekran Resmi 2022-02-25 01 07 46" src="https://user-images.githubusercontent.com/91700155/155763258-e4357f4a-2354-42fe-aeb9-ee6582417dff.png">

### 8- Launch the Instance
<img width="1435" alt="8" src="https://user-images.githubusercontent.com/91700155/155763281-6487a4dc-c577-4d35-bc94-299b92ff74eb.png">

### 9- Assign Elastic IP to Instance
<img width="1391" alt="Ekran Resmi 2022-02-25 01 09 42" src="https://user-images.githubusercontent.com/91700155/155763314-83988c4b-fc10-456a-aa4b-23d1d4108e7b.png">

### 10- Associate the elastic IP to the Instance

<img width="872" alt="Ekran Resmi 2022-02-25 01 11 38" src="https://user-images.githubusercontent.com/91700155/155763373-e217a856-8b0b-4e8e-b741-35c48be0ff5c.png">
<img width="871" alt="Ekran Resmi 2022-02-25 01 11 47" src="https://user-images.githubusercontent.com/91700155/155763378-eb35b1ae-0e62-4009-9e8e-618d63cd4b63.png">
<img width="1399" alt="Ekran Resmi 2022-02-25 01 12 17" src="https://user-images.githubusercontent.com/91700155/155763429-d4e84c62-1678-4cd6-935a-d32a5e826725.png">


### 11- Change the permission of Private Key
```console
chmod 400 <pem file name>.pem
```
<img width="1409" alt="Ekran Resmi 2022-02-25 01 32 26" src="https://user-images.githubusercontent.com/91700155/155763507-c230d07b-bb60-405b-9da0-35df5216dd00.png">

### 12- Connect using SSH
```console
ssh -i <pem file name> ubuntu@public-dns-name
```
<img width="1409" alt="Ekran Resmi 2022-02-25 01 32 26" src="https://user-images.githubusercontent.com/91700155/155763558-0888f594-c6cf-412f-97ba-2298f773f045.png">

### 13- Update the packages
```console
sudo apt update
sudo apt upgrade
```
<img width="1366" alt="Ekran Resmi 2022-02-25 01 34 10" src="https://user-images.githubusercontent.com/91700155/155763652-0b80d111-b32a-4ab2-af78-84c4085c6392.png">

### 14- Change Hostname to hadoop
```console
sudo nano /etc/hostname
```
<img width="1323" alt="Ekran Resmi 2022-02-25 01 37 49" src="https://user-images.githubusercontent.com/91700155/155763679-bdde4527-e3dc-41d5-b317-163cedda6cab.png">

### 15- Reboot and then Reconnect to Instance
```console
sudo reboot
```
<img width="1375" alt="Ekran Resmi 2022-02-25 01 39 39" src="https://user-images.githubusercontent.com/91700155/155763710-b778310a-d38e-457c-abe5-c8b4efbb5d38.png">

```console
ssh -i <pem file name> ubuntu@public-dns-name
```
<img width="1170" alt="Ekran Resmi 2022-02-25 01 40 10" src="https://user-images.githubusercontent.com/91700155/155763739-422e6a1c-70de-4716-816f-a0cee274a577.png">

### 16- Install Open JDK 8 
```console
sudo apt install openjdk-8-jdk
```
<img width="1171" alt="Ekran Resmi 2022-02-25 01 40 34" src="https://user-images.githubusercontent.com/91700155/155763760-be61b007-3bcd-4b0c-b047-892c5462313c.png">

### 17- Download and Install Hadoop
#### Go to Hadoop -> Downloads page
<img width="1338" alt="23" src="https://user-images.githubusercontent.com/91700155/155763798-8fafaa38-7baf-4603-aa53-d65fa4331cea.png">
<img width="1673" alt="24" src="https://user-images.githubusercontent.com/91700155/155765966-43a93163-5b04-4a42-8dbd-1e9b9b087530.png">

#### Install and extract the package
```console
wget <link> -P ~/Downloads
sudo tar zxvf ~/Downloads/hadoop-* -C /usr/local
```
<img width="1146" alt="Ekran Resmi 2022-02-25 01 42 38" src="https://user-images.githubusercontent.com/91700155/155763873-a53f5e16-f53f-485c-a199-187759330262.png">

### 18- Rename the folder
```console
sudo mv /usr/local/hadoop-* /usr/local/hadoop
```
<img width="1142" alt="Ekran Resmi 2022-02-25 01 44 25" src="https://user-images.githubusercontent.com/91700155/155763896-c497d89a-17d1-4b3b-a129-dd5a3c0af6bb.png">

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
```
<img width="1192" alt="Ekran Resmi 2022-02-25 01 44 56" src="https://user-images.githubusercontent.com/91700155/155763920-1906e25a-b90e-424a-ad7c-2c32a11103af.png">

#### For reflecting to current session
```console
source ~/.bashrc
```
<img width="1190" alt="Ekran Resmi 2022-02-25 01 46 52" src="https://user-images.githubusercontent.com/91700155/155763954-98a86040-f51a-4849-b851-1638391dfb6f.png">

#### Open hadoop-env.sh from $HADOOP_CONF_DIR
$
```console
sudo nano $HADOOP_CONF_DIR/hadoop-env.sh
```
<img width="1122" alt="Ekran Resmi 2022-02-25 01 53 17" src="https://user-images.githubusercontent.com/91700155/155763988-9b322ca9-2ab8-4df9-ac79-e7655f30661a.png">
<img width="1259" alt="Ekran Resmi 2022-02-25 01 50 01" src="https://user-images.githubusercontent.com/91700155/155764001-2f2005db-c068-4c9d-a249-264253e38ee2.png">

##### Change Java Home and Hadoop Conf Dir as below
```console
export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
export HADOOP_CONF_DIR=/usr/local/hadoop/etc/hadoop
```
<img width="1174" alt="Ekran Resmi 2022-02-25 01 51 23" src="https://user-images.githubusercontent.com/91700155/155764023-734d56fd-979c-4901-9950-88c02da69d42.png">

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

<img width="1124" alt="Ekran Resmi 2022-02-25 02 02 11" src="https://user-images.githubusercontent.com/91700155/155764070-a390a0be-381f-40d2-bbc6-f12e20a9f5c7.png">

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
<img width="1150" alt="Ekran Resmi 2022-02-25 02 04 54" src="https://user-images.githubusercontent.com/91700155/155764104-87260688-2095-40d2-ad13-7afb94f948d1.png">
<img width="479" alt="Ekran Resmi 2022-02-25 02 07 50" src="https://user-images.githubusercontent.com/91700155/155764112-ed91671c-f97b-402c-ade4-1b6f2f90e06c.png">

#### Copy the config and pem files to Instance .ssh directory
```console
scp ~/.ssh/config hadoop:~/.ssh
$ scp ~/.ssh/*.pem hadoop:~/.ssh
```

<img width="1221" alt="Ekran Resmi 2022-02-25 02 11 45" src="https://user-images.githubusercontent.com/91700155/155764149-6c116d77-d0e5-4098-a6e6-cf6aa606a1bb.png">

#### Reconnect to instance and create public key
```console
ssh -i <pem file name> ubuntu@public-dns-name
ssh hadoop
ssh-keygen -f ~/.ssh/id_rsa -t rsa -P ""
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
```
<img width="1139" alt="Ekran Resmi 2022-02-25 02 14 49" src="https://user-images.githubusercontent.com/91700155/155764182-ad380d97-5c29-40f2-af52-10f0a9983372.png">
<img width="568" alt="Ekran Resmi 2022-02-25 02 15 13" src="https://user-images.githubusercontent.com/91700155/155764217-f76bc945-91c8-4810-b7d9-2d5c599afecb.png">


#### Open /etc/hosts and add instance IPV4 address with hostname 
```console
sudo nano /etc/hosts
```
<img width="852" alt="Ekran Resmi 2022-02-25 02 17 08" src="https://user-images.githubusercontent.com/91700155/155764268-7f31b53c-3d37-47d3-9e74-2972f6d7acf9.png">


### 21- Hadoop Configuration
#### Edit core-site.xml
```console
sudo nano $HADOOP_CONF_DIR/core-site.xml
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

<img width="845" alt="Ekran Resmi 2022-02-25 02 19 29" src="https://user-images.githubusercontent.com/91700155/155764321-50e07b69-0fc5-49a8-8645-38eed43b1f0a.png">

#### Edit yarn-site.xml
```console
sudo nano $HADOOP_CONF_DIR/yarn-site.xml
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

<img width="846" alt="Ekran Resmi 2022-02-25 02 20 40" src="https://user-images.githubusercontent.com/91700155/155764344-679a2614-e820-4c82-bb77-0bcfb01adac2.png">


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

<img width="868" alt="Ekran Resmi 2022-02-25 02 21 57" src="https://user-images.githubusercontent.com/91700155/155764375-1014b0d0-271a-472e-af4d-b4f542f41a15.png">

#### Edit hdfs-site.xml
```console
sudo nano $HADOOP_CONF_DIR/hdfs-site.xml
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

<img width="872" alt="Ekran Resmi 2022-02-25 02 22 40" src="https://user-images.githubusercontent.com/91700155/155764405-c503fc8d-7cfd-45d7-a976-f0bc43eaf4a5.png">
<img width="865" alt="Ekran Resmi 2022-02-25 02 23 02" src="https://user-images.githubusercontent.com/91700155/155764439-44430c9c-12db-4c66-ba07-c34a922994fb.png">


#### Make namenode and datanode directories
```console
sudo mkdir -p $HADOOP_HOME/data/hdfs/namenode
sudo mkdir -p $HADOOP_HOME/data/hdfs/datanode
```
#### Change the owner 
```console
sudo chown -R ubuntu $HADOOP_HOME
```
#### Change masters and slaves to hadoop
```console
sudo nano $HADOOP_HOME/masters
sudo nano $HADOOP_HOME/slaves
```

<img width="869" alt="Ekran Resmi 2022-02-25 02 23 43" src="https://user-images.githubusercontent.com/91700155/155764463-2ac28915-61c7-4484-9290-0c578d5d482f.png">
<img width="867" alt="Ekran Resmi 2022-02-25 02 24 04" src="https://user-images.githubusercontent.com/91700155/155764476-7157698a-b13e-4f2f-b264-e97df77291db.png">
<img width="870" alt="Ekran Resmi 2022-02-25 02 24 24" src="https://user-images.githubusercontent.com/91700155/155764491-4f1c76b8-9c2e-49a3-8584-d4697ebeeab0.png">

### Launch Hadoop Cluster 
#### Format and start hdfs
```console
hdfs namenode -format
$HADOOP_HOME/sbin/start-dfs.sh
```
<img width="983" alt="Ekran Resmi 2022-02-25 02 58 10" src="https://user-images.githubusercontent.com/91700155/155764527-6391a4b9-3f7e-4202-adb1-4518bdb2187b.png">

#### Start yarn
```console
$HADOOP_HOME/sbin/start-yarn.sh
```
<img width="1000" alt="Ekran Resmi 2022-02-25 02 59 40" src="https://user-images.githubusercontent.com/91700155/155764560-f23b9a35-5ee6-4617-89a3-831a9349f73b.png">

#### Start the job history server
```console
$HADOOP_HOME/sbin/mr-jobhistory-daemon.sh start historyserver
```
#### To see the Java processes
```console
jps
```
<img width="748" alt="Ekran Resmi 2022-02-25 03 00 06" src="https://user-images.githubusercontent.com/91700155/155764614-662a8490-c763-4988-bc20-56e8214ef3a0.png">


### Accessing NameNode using WebUI
#### Namenode Overview
```console
publicdns:50070
```
<img width="1414" alt="Ekran Resmi 2022-02-25 03 01 17" src="https://user-images.githubusercontent.com/91700155/155764649-07f9e28d-a0f7-47a5-8312-28da3055ab73.png">

#### Cluster Metrics Overview
```console
publicdns:8088
```
<img width="1418" alt="Ekran Resmi 2022-02-25 03 01 36" src="https://user-images.githubusercontent.com/91700155/155764683-f7edd7c3-b8d2-4f5b-9543-85bcdf44ccc8.png">




# Running a sample mapreduce
### Creating an input file
```console
nano input
```
<img width="1009" alt="Ekran Resmi 2022-02-25 03 04 03" src="https://user-images.githubusercontent.com/91700155/155764722-42377337-a808-4b9f-8089-e6aa82b7a8e9.png">

### Creating a Directory in HDFS and Copying file from Local to HDFS
```console
hdfs dfs -mkdir -p WordCount/input
hdfs dfs -put input WordCount/input
```
### Running MapReduce
```console
hadoop jar $HADOOP_HOME/share/hadoop/mapreduce/hadoop-mapreduce-examples-2.8.5.jar wordcount WordCount/input WordCount/output
```
<img width="1010" alt="Ekran Resmi 2022-02-25 03 05 19" src="https://user-images.githubusercontent.com/91700155/155764751-f05a131c-ccff-4842-9ec3-99ac350ee86a.png">

### Output
```console
hdfs dfs -cat WordCount/output/part-r-00000
```

<img width="1007" alt="Ekran Resmi 2022-02-25 03 05 28" src="https://user-images.githubusercontent.com/91700155/155764791-16411777-3c25-40b5-99f4-54b6398339cc.png">


# Before logout, make sure to stop Hadoop services and AWS Instance
```console
$HADOOP_HOME/sbin/mr-jobhistory-daemon.sh stop historyserver
$HADOOP_HOME/sbin/stop-all.sh
```

<img width="1010" alt="Ekran Resmi 2022-02-25 03 06 39" src="https://user-images.githubusercontent.com/91700155/155764811-64c44502-095a-4154-a688-8093a7ee5975.png">



## Seda Atalay

