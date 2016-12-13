# MapReduce-for-MODAC
Implements method as described here https://arxiv.org/abs/1611.06208. Provides mapper and reducer functions for Hadoop cluster.

This code has been tested on Flux Hadoop cluster at the University of Michigan. Below are some useful commands for natigating through hdfs and Linux.

# navigate to working directory (where you store map.py and red.py)
cd testflux/modac

# copy the input folder onto hdfs
hdfs dfs -copyFromLocal input input
hdfs dfs -ls

# run map reduce job, with 1 reducer (in this way we can get a combined estimate)
yarn jar /usr/lib/hadoop-mapreduce/hadoop-streaming.jar -Dmapreduce.job.queuename=default -input input -output output -mapper map.py -reducer red.py -file map.py -file red.py -numReduceTasks 1 -partitioner org.apache.hadoop.mapred.lib.KeyFieldBasedPartitioner

# receive output to local directory and delete fild on hdfs
```
hdfs dfs -get output output
hdfs dfs -rm -r -skipTrash output
```
