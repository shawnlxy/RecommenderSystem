# RecommenderSystem
Description: This project implements Item Collaborative Filtering(Item CF) algorithm with mapreduce, which chains 5                      mapreduce jobs
             Job 1 : Build co-occurrence matrix
             Job 2 : Normalize co-occurrence matrix
             Job 3 : Build rating matrix
             Job 4 : Multiply co-occurrence matrix and rating matrix
             Job 5 : Generate recommender list

Environment: Hadoop + Docker

****************
Command Guide:

enter hadoop

cd src

git clone https://github.com/shawnlxy/RecommenderSystem.git

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
