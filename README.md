# RecommenderSystem
Environment: Hadoop + Docker

enter hadoop

cd src


tar -xvf  RecommenderSystem.tar 

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
