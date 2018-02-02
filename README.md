# RecommenderSystem
This project implements Item Collaborative Filtering(Item CF) algorithm with mapreduce, which chains 5 mapreduce jobs.

```
Build co-occurrence matrix

Normalize co-occurrence matrix

Build rating matrix

Multiply co-occurrence matrix and rating matrix

Sum up multiplication for each user

```
## Prerequisites 

* [Docker](https://docs.docker.com/) - Container

### How to build hadoop cluster on Docker

```
$ mkdir bigdata
$ cd bigdata
$ sudo docker pull joway/hadoop-cluster 
$ git clone https://github.com/joway/hadoop-cluster-docker 
$ sudo docker network create --driver=bridge hadoop 
$ cd hadoop-cluster-docker

$ sudo ./start-container.sh

$ ./start-hadoop.sh
```


## Get Started:
Download project:
```
$ cd ~/src
$ git clone https://github.com/shawnlxy/RecommenderSystem.git
```
Enter hadoop:
```
$ cd hadoop-cluster-docker
$ ./start-container.sh
$ ./start-hadoop.sh
$ cd src
```
HDFS operations:

```
cd RecommenderSystem 

hdfs dfs -mkdir /input

hdfs dfs -put input/* /input  # upload users' rating records

hdfs dfs -rm -r /dataDividedByUser

hdfs dfs -rm -r /coOccurrenceMatrix

hdfs dfs -rm -r /Normalize

hdfs dfs -rm -r /Multiplication

hdfs dfs -rm -r /Sum

cd src/main/java/

hadoop com.sun.tools.javac.Main *.java

jar cf recommender.jar *.class

hadoop jar recommender.jar Driver /input /dataDividedByUser /coOccurrenceMatrix /Normalize /Multiplication /Sum

#args0: original dataset

#args1: output directory for DividerByUser job

#args2: output directory for coOccurrenceMatrixBuilder job

#args3: output directory for Normalize job

#args4: output directory for Multiplication job

#args5: output directory for Sum job

hdfs dfs -ls /

hdfs dfs -cat /Sum/*

```
