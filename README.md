Explain Hadoop Deployment Layout in Brief.


There are many components of the hadoop ecosystem. By default some there are some components with which hadoop can function upto minimal requirements, but to deploy hadoop into a cluster i.e into each and every machine in the cluster in a fully functional manner one has to have a fixed set of components 

*The components needed are mentioned below:
- Hadoop Common - Common including the native code and required jar files. 
- HDFS Client - HDFS jars, scripts, and shared libraries. 
- HDFS Server - jsvc executable 
- Yarn Client - Yarn client jars and scripts 
- Yarn Server - Yarn server jars and scripts 
- MapReduce - MapReduce jars, scripts, and shared libraries 
- LZO - LZ0 codec from github.com/omally/hadoop-gpl-compression 
- Metrics - Plugins for Chukwa and Ganglia 

*Packages from other teams will include:
- Pig 
- Hive 
- Oozie client 
- Oozie server 
- Howl client 
- Howl server 
Above list is taken from hadoop deployment layout from apache.org

The deployment should be as generalized as possible i.e the insatlling of the packages should be independent of the package manager i.e the they should be able to be installed with YUM package manager or they should be able to be insatlled in ubuntu etc.

**The Attached is the pictorial representation of the deployed hadoop ecosystem.


In the book hadoop cluster deployment  by Daniel Zburivsky 
he tells the steps the in the deplayment of the hadoop cluster


1)Setting up hadoop cluster
- choosing the cluster hardware
-hadoop distributions
- choosing os for hadoop cluster.

2)Insatlling and configuring hadoop
-configuring the os.
-setting up the name node.

3) configuring the hadoop ecosystem.
-scoop 
-hive
-impala

4) securing the hadoop installation
-security overview
-hdfs security
-mapreduce security
etc.

5)Monitoring hadoop cluster
-monitoring hadoop using ganglia

6)deploying hadoop on cloud
- Amazon elastic mapreduce

Here are the top level directories and a sample of what would be under each. Note that all of the packages are installed "flattened" into the prefix directory. For compatibility reasons, we should create "share/hadoop" that matches the old HADOOP_HOME and set the HADOOP_HOME variable to that.
$PREFIX/ bin / hadoop
               |     | mapred
               |     | pig -> pig7
               |     | pig6
               |     + pig7
               |
               + etc / hadoop / core-site.xml
               |              | hdfs-site.xml
               |              + mapred-site.xml
               |
               + include / hadoop / Pipes.hh
               |         |        + TemplateFactory.hh
               |         + hdfs.h
               |
               + lib / jni / hadoop-common / libhadoop.so.0.20.0
               |     |
               |     | libhdfs.so -> libhdfs.so.0.20.0
               |     + libhdfs.so.0.20.0
               |
               + libexec / task-controller
               |
               + man / man1 / hadoop.1
               |            | mapred.1
               |            | pig6.1
               |            + pig7.1
               |
               + share / hadoop-common 
               |       | hadoop-hdfs
               |       | hadoop-mapreduce
               |       | pig6
               |       + pig7
               |
               + sbin / hdfs-admin
               |      | mapred-admin
               |
               + src / hadoop-common
               |     | hadoop-hdfs
               |     + hadoop-mapreduce
               |
               + var / lib / data-node
                     |     + task-tracker
                     |
                     | log / hadoop-datanode
                     |     + hadoop-tasktracker
                     |
                     + run / hadoop-datanode.pid
                           + hadoop-tasktracker.pid
Path can be configured at compile phase or installation phase. For RPM, it takes advantage of the --relocate directive to allow path reconfiguration at install phase. For Debian package, path is configured at compile phase.
